---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - javascript

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction asdf

Welcome to the CMC/ESM API! You can use our API to access CMC/ESM API endpoints.

We have language examples in Shell and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This API documentation page was created with [Slate](https://github.com/lord/slate).

# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "https://metals.performance-software.com/api/endpoint/here/export.json" \
  -H "CMC-Authorization: abcd-efg-hijk-lmnop"
```

```javascript
const axios = require('axios');

let config = {
  'headers': {
    'CMC-Authorization': 'abcd-efg-hijk-lmnop'
  }
};

axios.get('https://metals.performance-software.com/api/endpoint/here/export.json', config)
.then((response) => {
  console.log(response);
})
.catch((error) => {
  console.log(error);
});
```

> Make sure to replace `abcd-efg-hijk-lmnop` with your API key.

CMC/ESM uses API keys to allow access to the API. You can register a new CMC/ESM API contacting our developers.

CMC/ESM expects for the API key to be included in all API requests to the server in a header that looks like the following:

`CMC-Authorization: abcd-efg-hijk-lmnop`

<aside class="notice">
You must replace <code>abcd-efg-hijk-lmnop</code> with your personal API key.
</aside>
<aside class="notice">
This documentation will utilize the Axios library for javascript/node related examples to handle network requests
</aside>
- [Axios](https://github.com/axios/axios)

# API Breakdown

## Further Documentation

Below are links to further documentation divided by system functionality.

System Function | Description
--------- | -----------
[General Record Retrieval](https://metals.performance-software.com/file-system-documentation) | This API Documentation explains how to access individual ERP system records as well as explanations of system interactions, files and data.
[Scheduling](https://metals.performance-software.com/scheduling-documentation) | This API Documentation describes available reports related to Production Scheduling

# GET and POST requests and argument structure

## Using URL query

```shell
# With shell, you can just pass the correct header with each request
curl "https://metals.performance-software.com/api/endpoint/here/export.json?arg1=value1&arg2=value2" \
  -H "CMC-Authorization: abcd-efg-hijk-lmnop"
```

```javascript
const axios = require('axios');

let config = {
  'headers': {
    'CMC-Authorization': 'abcd-efg-hijk-lmnop'
  }
};

axios.get('https://metals.performance-software.com/api/endpoint/here/export.json?arg1=value1&arg2=value2', config)
.then((response) => {
  console.log(response);
})
.catch((error) => {
  console.log(error);
});
```

- Using the URL query is useful for non-complex data structures. After the '?' in the URL you can assign key value pairs delimited by the '&'.

- You MUST remember to encode each key/value pair in the query string using []% encoding](https://www.w3schools.com/jsref/jsref_encodeuricomponent.asp)

- Data within data will have to use HTTP POSTs as shown in the next section

## Using HTTP POST

```shell
# With shell, you can just pass the correct header with each request
curl -X POST "https://metals.performance-software.com/api/endpoint/here/export.json" \
  -H "CMC-Authorization: abcd-efg-hijk-lmnop" \
  -d "{ \
        'arg1': 'value1', \
        'arg2': 'value2', \
        'arg3': { \
          'innerArg1': 'value' \
        } \
      }"
```

```javascript
const axios = require('axios');

let config = {
  'headers': {
    'CMC-Authorization': 'abcd-efg-hijk-lmnop'
  }
};

let data = {
  'arg1': 'value1',
  'arg2': 'value2',
  'arg3': {
    'innerArg1': 'value'
  }
};

axios.post('https://metals.performance-software.com/api/endpoint/here/export.json', data, config)
.then((response) => {
  console.log(response);
})
.catch((error) => {
  console.log(error);
});
```

For more complex requests/submissions requiring large data, a URL is limiting. For this, use HTTP POSTs and include JSON as the data to POST. EZgen will parse complex JSON and utilize it in the request if necessary.

# Tables/Lists

## Tables/Lists default behavior

```json
{
  "process_time": 0.040123,
  "requestID": 45041,
  "success": true,
  "format": [
    {
      "Header": "File Number",
      "accessor": "FileNumber",
      "description": "File Number",
      "id": "FileNumber"
    }, {
      "Header": "File Name",
      "accessor": "FileName",
      "description": "File Name",
      "id": "FileName"
    }, {
      "Header": "Last Modified",
      "accessor": "LastModified",
      "description": "Last Modified Date",
      "flexGrow": 1,
      "id": "LastModified",
      "minWidth": 400,
      "multiplier": 1000,
      "type": "date",
      "width": 400
    }, {
      "Header": "Record Count",
      "accessor": "RecordCount",
      "description": "Record Count",
      "id": "RecordCount",
      "type": "number"
    }
  ],
  "lines": [
    {
      "FileName": "A FILE",
      "FileNumber": 1,
      "LastModified": 0,
      "RecordCount": 0
    },
    ...
  ]
}
```

Tables are an important part of the API. When requesting a list of records from any API there are certain features you can expect to be there by default.

The JSON to the right is an example table of data retrieved from the List Files API: [List Files](https://metals.performance-software.com/file-system-documentation/#files). There are several items in this API result that you can expect from all list results like it.

Field | Description
--------- | -----------
success | Did the EZgen system succeed in fulfilling the request. If this is true, then EZgen processed the request successfully. If false, it means that EZgen found something wrong with the request and will show an error description in a field called ```error``` and ```error_text```. If an HTTP error is returned such as a 502, this means EZgen may have succeeded but a network or system outage is preventing the response from reaching the user.
requestID | The ID of the API Request. This is the key value for a record in the (API REQUEST FILE)[https://metals.performance-software.com/#/app/file-system/api-usage] that has additional details about the request.
process_time | How long did the API take to execute
format | This is an array of column headers and associated information. This ordered array represents what columns this report will have from left to right. The ```Header``` field represents the column header text and the ```id``` represents the corresponding field name in the ```lines``` array that will display the data per row
lines | This is an array of the rows in the table. This ordered array represents each row of data to be displayed in the table. Use the ```id``` field in each column header to identify which column to place each field within the row and use associated meta data from the ```format``` array to further describe it.
