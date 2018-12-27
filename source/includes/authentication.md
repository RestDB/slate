# Authentication
API calls against your database REST API must be authenticated. 
> Example code for an authenticated API call:

```shell
# With shell, you can just pass the correct header with each request
curl -k -i -H "Content-Type: application/json"\
 -H "x-apikey: MY-API-KEY-HERE"\
 -X GET 'https://{mydatabase}.restdb.io/rest/people'
```

> Make sure to replace `MY-API-KEY-HERE` with your actual API key.

Authentication can be done with one of the following methods:

* **API key** as a query parameter, e.g. `?apikey=xxxxx`
* **API key** as a HTTP header field, e.g. `x-apikey=xxxxx`
* **Signed JWT token** as a HTTP header field, `Authorization=Bearer xxxxx`


You can create your API keys on the admin dashboard of your database, shown in the example screenshot below.

![admin dashboard](https://ras-blogdb.restdb.io/media/5bfe8b971c8eea7400002e95)



## CORS API keys
> Ajax call via CORS:

```shell
No example i cURL here.
```

```hbs
No example i HTML/Handlebars here.
```

```js
// Call API from a web browser requires a CORS enabled API key
var myCorsApiKey = "{MY-CORS-API-KEY-HERE}";
var data = null;

var xhr = new XMLHttpRequest();
xhr.withCredentials = true;

xhr.addEventListener("readystatechange", function () {
  if (this.readyState === 4) {
    console.log(this.responseText);
  }
});

xhr.open("GET", "https://{mydatabase}.restdb.io/rest/people");
xhr.setRequestHeader("content-type", "application/json");
xhr.setRequestHeader("x-apikey", myCorsApiKey);
xhr.setRequestHeader("cache-control", "no-cache");

xhr.send(data);
```

To connect to your database from a web page, a valid Ajax call with CORS must be done. CORS (cross-origin resource sharing) manages cross-origin requests. A CORS enabled API-key controls who can access the database and valid HTTP verbs agaists a data resource, i.e. `GET`, `POST`, `PUT`, `PATCH` and `DELETE`.

You can manage your API-keys unders the Settings/API tab.

![CORS settings](https://ras-blogdb.restdb.io/media/5603c3353c55510300000004?s=w)



## Auth0.com JWT tokens

```shell
No example i cURL here.
```

```handlebars
No example i HTML/Handlebars here.
```

```javascript
var AUTH0_CLIENT_ID='xxx'; 
var AUTH0_DOMAIN='xxx';
var AUTH0_CALLBACK_URL=location.href;

// invoke the lock component
var lock = new Auth0Lock(AUTH0_CLIENT_ID, AUTH0_DOMAIN, {
    auth: {
      params: { scope: 'openid email' } //Details: https://auth0.com/docs/scopes
    },
    rememberLastLogin: true
  });

  $('.btn-login').click(function(e) {
    e.preventDefault();
    lock.show();
  });

  lock.on("authenticated", function(authResult) {
    lock.getProfile(authResult.idToken, function(error, profile) {
        if (error) {
            alert("Unable to authenticate!");
            return;
        }
        localStorage.setItem('id_token', authResult.idToken);
        // Display user information
        show_profile_info(profile);
        // enable api button
        $('.btn-api').removeAttr("disabled").text("Press me, I'm authenticated!");
    });
  });

// We use the token from Auth0 to authenticate API calls against restdb.io databases
// by setting the Authorization header using the Bearer token scheme.

  $('.btn-api').click(function(e) {
    fetch("https://{mydatabase}.restdb.io/rest/items?max=4",{
    headers:{
        'Authorization':'Bearer ' + localStorage.getItem("id_token")
        }
    }).then(response=>{
        return response.json();
    }).then(body=>{
         $('#apidata').text(JSON.stringify(body, null, '  '));
    });
    e.preventDefault();
  });
```

RestDB supports direct integration with the auth0.com authentication service. JWT ([JSON Web Token](https://jwt.io/)) are signed with your Auth0 secret and verified by RestDB using the same secret.
Auth0.com lets you add a multitude of authentication schemes to your app.
![Auth0.com lock component](https://ras-blogdb.restdb.io/media/57d1327a791a484c000001d2?s=o&key=327688688052565719837)

You can manage the Auth0.com integration and settions under Settings/Authentication.

![Auth0.com secret](https://ras-blogdb.restdb.io/media/5c04e23f587d725400000745?s=w)

<a target="restdb" href="https://restdb.io/blog/57cece1a2d5dbc27000000d3">Blog post with a complete demo application here.</a>


## Custom JWT API
Issue a new signed JWT with custom claims.

```javascript
No example i Javascript here.
```

```handlebars
No example i HTML/Handlebars here.
```

```shell
curl -X POST \
  https://{mydatabase}.restdb.io/auth/jwt \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-apikey: 021ead58943f10990f5b9b50b5e884f11bf00' \
  -d '{
	"secret": "google.private_key",
	"algorithm": "RS256",
	"issuer": "server@xxx-yyy.iam.gserviceaccount.com",
	"audience":"https://www.googleapis.com/oauth2/v4/token",
	"subject": "name@example.com",
	"expiresIn": "1h",
	"payload":{
		"scope":"https://www.googleapis.com/auth/gmail.readonly"
		
	}
}'
```

> Example output

```json
{
    "jwt": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzY29wZSI6Imh0dHBzOi8vd3d3Lmdvb2dsZWFwaXMuY29tL2F1dGgvZ21haWwucmVhZG9ubHkiLCJpYXQiOjE1NDU4MTg0MDYsImV4cCI6MTU0NTgyMjAwNiwiYXVkIjoiaHR0cHM6Ly93d3cuZ29vZ2xlYXBpcy5jb20vb2F1dGgyL3Y0L3Rva2VuIiwiaXNzIjoic2VydmVyQHh4eC15eXkuaWFtLmdzZXJ2aWNlYWNjb3VudC5jb20iLCJzdWIiOiJuYW1lQGV4YW1wbGUuY29tIiwianRpIjoiY21WemRHUmliV0ZwYkMwek5HRTRMbkpsYzNSa1lpNXFkM1F1YlhselpXTnlaWFF2TnprMU1tRXlZbVUyWVRJM09XWTNZbVJqWkRreE56ZzRaVGhoWmpsbE1UQT0ifQ.s3prKE3UO16oRhVVO9uZ-Tn8K1mF6Z6vpKGQrNwxxxM",
    "refresh": "853948951eca9da241e642d5c9b0383abba55571a8995e67f64e8b55eea36f53"
}
```

**HTTP REQUEST**


`POST https://{mydatabase}.restdb.io/auth/jwt`

The `POST` body Request body contains JWT settings and claims.

**ARGUMENTS**

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
`secret` | `string` | Mandatory | Path to settings property
`algorithm` | `string` | Optional | Hash algo

<aside class="warning">
*HTTPS is required. The restdb.io database REST API only responds to encrypted traffic so that your data remains safe. All API traffic must have a valid apikey or a JWT token.
</aside>