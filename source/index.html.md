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
  - <a href='https://restdb.io'>Sign Up for a new RestDB account here</a>
  
includes:
  - collection-api.md
  - mail-api.md
  - media-api.md
  - metadata-api.md
  - codehook-api.md
  - javascript-api.md
  - plugin-api.md
  - realtime-api.md
  - snapshot-api.md
  - pages.md
  - webhooks.md
  - custom-routes.md
  - relations.md
  - command-line.md
  - debugging.md
  - app-settings.md
  - caching.md
  - errors

search: true
---
# Introduction
This is the RestDB developer documentation and API reference.

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


