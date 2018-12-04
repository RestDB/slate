# Authentication
API calls against your database REST API must be authenticated. Authentication can be done with one of the following methods:

* **JWT token** as a HTTP header field, `Authorization=Bearer xxxxx`
* **API key** as a query parameter, e.g. `?apikey=xxxxx`
* **API key** as a HTTP header field, e.g. `x-apikey=xxxxx`


> Example code for an authenticated API call:

```shell
# With shell, you can just pass the correct header with each request
curl -k -i -H "Content-Type: application/json"\
 -H "x-apikey: MY-API-KEY-HERE"\
 -X GET 'https://{mydatabase}.restdb.io/rest/people'
```

> Make sure to replace `MY-API-KEY-HERE` with your actual API key.

You can create your API keys on the admin dashboard of your database, shown in the example screenshot below.

![admin dashboard](https://ras-blogdb.restdb.io/media/5bfe8b971c8eea7400002e95)

<aside class="warning">
For security reasons, only HTTPS is allowed for connecting to your database API.
</aside>


## CORS API keys
bla bla bla.

> CORS code:


```javascript
// Call API from a web browser requires a CORS enabled API key
```
> CORS is fun.

## JWT tokens
bla bla bla

## Auth0 integration
bla bla bla

## Users and secure tokens API  


**HTTP REQUEST**

```shell
bin bash
```

> Example output
```json
{
  "data": "value"
}
```

`POST https://{mydatabase}.restdb.io/auth/token`

The `POST` body Request body can be an access token or JWT token.

**ARGUMENTS**

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
code | String | Optional | your access code
refresh | String | Optional | Your JWT token

<aside class="warning">
*HTTPS is required. The restdb.io database REST API only responds to encrypted traffic so that your data remains safe. All API traffic must have a valid apikey or a JWT token.
</aside>