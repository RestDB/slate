---
title: RestDB API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript--node: Node.js
  - javascript--browser: JS
  - python: Python
  - php: PHP
  - java: Java
  - csharp: C#
  - swift: Swift

toc_footers:
  - <a href='https://restdb.io'>Sign Up for a new Database</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---
# Introduction
bla bla bla

# Authentication

> To authorize, use this code:

```java
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

```swift
import Foundation

let headers = [
"content-type": "application/json",
"x-apikey": "560bd47058e7ab1b2648f4e7",
"cache-control": "no-cache"
]

let request = NSMutableURLRequest(url: NSURL(string: "https://inventory-fac4.restdb.io/rest/motorbikes")! as URL,
                                        cachePolicy: .useProtocolCachePolicy,
                                        timeoutInterval: 10.0)
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

```csharp
let cors = charpcode;
```
> Some code annotation goes here.

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

<aside class="warning">
*HTTPS is required. The restdb.io database REST API only responds to encrypted traffic so that your data remains safe. All API traffic must have a valid apikey or a JWT token.
</aside>


# Database collection REST API

The [Restful](https://en.wikipedia.org/wiki/Representational_state_transfer) API automatically reflects your database schema. All restdb.io databases have a unique URL as a REST endpoint. Client applications communicate through the URL with JSON objects. A database collection (same as a SQL table) contains your JSON documents. 

## GET data from a collection

`GET https://{mydatabase}.restdb.io/rest/{collection}[?query parameters]`


```shell
# With shell, you can just pass the correct header with each request
curl -X GET \
  'https://sports-xf03.restdb.io/rest/companies?q={%22status%22:%20%22professional%22}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-apikey: 73bf145c901d1feecf80c26a9d0d1a64aa145'
```

```javascript--node
// Node.js Javascript
var request = require("request");

var options = { method: 'GET',
  url: 'https://sports-xf03.restdb.io/rest/players',
  qs: { q: '{"status": "professional"}' },
  headers: 
   { 'cache-control': 'no-cache',
     'x-apikey': '73bf145c901d1fcece81c26a9d0d1a64aa145',
     'Content-Type': 'application/json' } };

request(options, function (error, response, body) {
  if (error) throw new Error(error);

  console.log(body);
});
```

```javascript--browser
// Browser version
var data = null;

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", 'https://sports-xf03.restdb.io/rest/players?q={"status": "professional"}');
xhr.setRequestHeader("Content-Type", "application/json");
xhr.setRequestHeader("x-apikey", "73bf145c901d1fcece81c26a9d0d1a64aa145");
xhr.setRequestHeader("cache-control", "no-cache");

xhr.send(data);
```

```python
Python code here...
```

```java
Java code here...
```

```php
PHP code here...
```

```csharp
C# code here...
```

```swift
Swift code here...
```

> The above queries result in the following JSON array output.

```json
[
  {
    "name": "Jones",
    "status": "professional",
    "score": 42
  }
]
```


### URL Parameters

Parameter | Description
--------- | -----------
`{mydatabase}` | Your unique database name, e.g. `sports-xf03`
`{collection}` | A unique collection name in your database, e.g. `players`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
q | `{}` | Database Query. JSON format
h | `{}` | [Query hints](#query-hints) for Query and output. JSON format
filter | | Free text search filter
sort | `_id` | Field to sort query result on
dir | `-1` | Sort direction, -1 = ascending, 1 = descending
skip | `0` | Skip forward in result data set
max | `1000` | Data result page size
metafields |  | Add system fields in data result. See [meta fields](#meta-fields)
totals | | Return data and paging meta data. See [data result paging](#data-result-paging)
groupby || Group data by field
aggregate || Aggregae data by field
apikey || Add an apikey in as request parameter instead of as a header value (not recommended)
idtolink || URLs for links and images
flatten || Place deep properies on root object
referencedby || refs
fetchmediadata || media
fetchchildren || child data
format || .js or .html

### Data result paging
Use the totals query parameter to retrieve data about totals, page size and page skipping.

The example query URL below shows an example:

`GET https://sports-xf03.restdb.io/rest/companies?totals=true&skip=10&max=2`

> Data result paging output example below:

```json
{
    "data": [
        {
            "_id": "5631d356f941f479000000ea",
            "name": "Fames Institute",
            "address": "8557 Elit, Rd.",
            "city": "Goslar",
            "zip": "Z2 8KA"
        },
        {
            "_id": "5631d356f941f47900000109",
            "name": "Urna LLP",
            "address": "P.O. Box 108, 7946 Erat Avenue",
            "city": "Morpeth",
            "zip": "K1Z 2TI"
        }
    ],
    "totals": {
        "total": 102,
        "count": 2,
        "skip": 10,
        "max": 2
    }
}
```

## Query language
bla bla

### Logic
bla bla

### Aggregation
bla bla

### Header values
bal bla

### Query hints
bla bla hints

### Meta fields
`_keywords`, `_tags`, `_version`, `_created`, `_createdby`, `_mock`


## POST resource
bla bla

### Data payload
bla bla

### Using POST to emulate PUT, DELETE, PATCH
If your development platform or firewall rules prevent you from calling HTTP methods like PUT, PATCH or DELETE, use the `X-HTTP-Method-Override` header. Pass the method you want to use in the X-HTTP-Method-Override header and make your call using the POST method.




# Real time API
bla bla


# Media Content API

Read more about media archive [here](https://restdb.io/docs/media-archive).

# Meta Data API  

# Mail API  

Read more [about mail API here](https://restdb.io/docs/mail-api#restdb).

# JavaScript API

bla bla

# Plugin API

bla bla

# Codehook API
bla bla

# Snapshot API
bla bla

# Relations in data
bla bla

## Lookups
bla bla

## Parent child
bla bla


# Custom routes
bla bla


# Webhooks

bla bla

# Application settings
bla bla

## Caching
bla bla

## Properties
bla bla

# Pages
bla bla

## Handlebars
bla bla

## Variables
bla bla

## Page Codehooks
bla bla

# Command line tool
bla bla

# Debugging
bla bla

## Rest inspector
bla bla

## Realtime output
bla bla

## Web console
bla bla

