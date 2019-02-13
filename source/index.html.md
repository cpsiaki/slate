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

# Introduction

Welcome to the CMC/ESM API! You can use our API to access CMC/ESM API endpoints.

We have language examples in Shell and JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

This API documentation page was created with [Slate](https://github.com/lord/slate).

# Authentication

```shell
# With shell, you can just pass the correct header with each request
curl "https://metals.performance-software.com/api/endpoint/here"
  -H "CMC-Authorization: abcd-efg-hijk-lmnop"
```

```javascript
const axios = require('axios');

let headers = {
  'CMC-Authorization': 'abcd-efg-hijk-lmnop'
};
console.log(axios.get('/api/endpoint/here', headers));
```

> Make sure to replace `abcd-efg-hijk-lmnop` with your API key.

CMC/ESM uses API keys to allow access to the API. You can register a new CMC/ESM API contacting our lead developers.

CMC/ESM expects for the API key to be included in all API requests to the server in a header that looks like the following:

`CMC-Authorization: abcd-efg-hijk-lmnop`

<aside class="notice">
You must replace <code>abcd-efg-hijk-lmnop</code> with your personal API key.
</aside>

# API Breakdown

## Further Documentation

Below are links to further documentation divided by system functionality.

### Query Parameters

System Function | Description
--------- | -----------
[General Record Retrieval](https://metals.performance-software.com/file-system-documentation) | This API Documentation explains how to access individual ERP system records as well as explanations of system interactions, files and data.
[Scheduling](https://metals.performance-software.com/scheduling-documentation) | This API Documentation describes available reports related to Production Scheduling
