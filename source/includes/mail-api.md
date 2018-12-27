# Mail API  
REST endpoint for sending emails. Email sending is relayed through Mailgun or Gmail APIs.
You can add your own accounts for Mailgun or Gmail.

## Send an email

```shell
curl -X POST \
  https://devdemo-ff5b.restdb.io/mail \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-apikey: xxxxxxxxx' \
  -d '{
    "to":"jones@restdb.io",
    "subject":"Trigger email from you database", 
    "html": "Hello email world!"
}'
```

> Example response (201)

```json
{
    "result": [
        {
            "email_outbound_id": "5bdc50a874ae8c710000dd16"
        }
    ],
    "warning": "For development plan: Max 2 emails in arrays, no templates, no Gmail transport. Upgrade plan for these features."
}
```

**HTTP REQUEST**

`POST https://{mydatabase}.restdb.io/mail`

The `POST`body can be a single email JSON object `{arguments}`, or an array of email JSON objects `[{...}, {...}]`.

**ARGUMENTS**

Parameter | Type | Required | Description
--------- | ---- | -------- | -----------
to | String | Required | One valid receiver email address
subject | String | Optional | Email subject text line
html | String or JSON | Required | Email body
company | String | Optional | Email footer in the default template
sendername | String | Optional | Display name for the email sender address
transport | String | Optional | Blank or `"Gmail"`. Gmail requires a paid plan
template | String | Optional | A Page name with the template html content

## List sent emails

> Get sent emails (200)

```json
{
    "_id": "5bdc50a874ae8c710000dd16",
    "to": "jones@restdb.io",
    "status": "sent",
    "transport": "restdb_mailer",
    "from": "no-reply@mg.restdb.ws",
    "subject": "Trigger email from you database",
    "company": "",
    "unsubscribelink": "",
    "_dbname": "devdemo-ff5b",
    "track": "5bdc50a874ae8c710000dd16",
    "body": "Hello email world!",
    "tracking-status": "read",
    "tracking-date": "2018-11-02T13:32:16.633Z"
}
````

`GET https://devdemo-ff5b.restdb.io/rest/email_outbound`

## Get one sent email

`GET https://devdemo-ff5b.restdb.io/rest/email_outbound/{ID}`

Read more [about mail API here](https://restdb.io/docs/mail-api#restdb).