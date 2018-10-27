---
title: RestDB API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='https://restdb.io'>Sign Up for a new Database</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---
# Authentication with your RestDB database

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('MY-API-KEY-HERE')
```

```python
import kittn

api = kittn.authorize('MY-API-KEY-HERE')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: MY-API-KEY-HERE"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('MY-API-KEY-HERE');
```

> Make sure to replace `MY-API-KEY-HERE` with your API key.

RestDB uses API keys to allow access to the API. You can register a new API key at our [developer portal](http://example.com/developers).

RestDB expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: MY-API-KEY-HERE`

<aside class="notice">
You must replace <code>MY-API-KEY-HERE</code> with your personal API key.
</aside>


## CORS API keys
bla bla bla.

> CORS code:

```ruby
cors = Kittn::APIClient.poff!('MY-API-KEY-HERE')
```

```python
api = kittn.authorize('MY-API-KEY-HERE')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: MY-API-KEY-HERE"
```

```javascript
let api = kittn.authorize('MY-API-KEY-HERE');
```
> CORS is fun.

## JWT tokens
bla bla bla

## Auth0 integration
bla bla bla

# REST database API

One of the core features of the restdb.io database cloud service is the [Restful](https://en.wikipedia.org/wiki/Representational_state_transfer) API which automatically reflects your database schema. All restdb.io databases have a unique URL as a REST endpoint. Client applications communicate through the URL with JSON objects. A database collection (same as a SQL table) contains your JSON documents. 

<aside class="notice">
*HTTPS is required. The restdb.io database REST API only responds to encrypted traffic so that your data remains safe. All API traffic must have a valid apikey or authorization [JWT](https://en.wikipedia.org/wiki/JSON_Web_Token) token as a parameter or as a request header field.*
</aside>

Read more about [how to query database here](https://restdb.io/docs/querying-with-the-api).

Code examples for [popular programming languages here.](https://restdb.io/docs/rest-api-code-examples#restdb)

## Using POST to emulate PUT, DELETE, PATCH
If your development platform or firewall rules prevent you from calling HTTP methods like PUT, PATCH or DELETE, use the `X-HTTP-Method-Override` header. Pass the method you want to use in the X-HTTP-Method-Override header and make your call using the POST method.

## Media Content API


Read more about media archive [here](https://restdb.io/docs/media-archive).

## Meta Data API  

## Mail API  

Read more [about mail API here](https://restdb.io/docs/mail-api#restdb).

## Quick example

For our test database,  the REST endpoint URL is:

`https://rdb-simpledb.restdb.io/rest`


