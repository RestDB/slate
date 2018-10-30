---
title: RestDB API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell: cURL
  - javascript: JavaScript
  - python: Python
  - java: Java
  - csharp: C# (.NET)
  - swift: Swift (iOS)

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


# Database REST API

The [Restful](https://en.wikipedia.org/wiki/Representational_state_transfer) API automatically reflects your database schema. All restdb.io databases have a unique URL as a REST endpoint. Client applications communicate through the URL with JSON objects. A database collection (same as a SQL table) contains your JSON documents. 


## GET resource
bla bla

### Header values
bal bla

## POST resource
bla bla

### Data payload
bla bla

<aside class="information">
Using POST to emulate PUT, DELETE, PATCH
If your development platform or firewall rules prevent you from calling HTTP methods like PUT, PATCH or DELETE, use the `X-HTTP-Method-Override` header. Pass the method you want to use in the X-HTTP-Method-Override header and make your call using the POST method.
</aside>


## Query language
bla bla

### Logic
bla bla

### Aggregation
bla bla


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

