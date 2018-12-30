
# Data Collection API

The [Restful](https://en.wikipedia.org/wiki/Representational_state_transfer) API automatically reflects your database schema. All restdb.io databases have a unique URL as a REST endpoint. Client applications communicate through the URL with JSON objects. A database collection (same as a SQL table) contains your JSON documents. 

## Query data


> Example code to GET data list from a collection:

```shell
curl -g -X GET \
  'https://sports-xf03.restdb.io/rest/companies?q={"status":"professional"}&sort=score&max=10' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-apikey: 73bf145c901d1feecf80c26a9d0d1a64aa145'
```

> Example output:

```json
[
  {
    "name": "Jane",
    "status": "professional",
    "score": 9
  },
  {
    "name": "Joey",
    "status": "professional",
    "score": 6
  }
]
```
**HTTP REQUEST**

`GET https://{mydatabase}.restdb.io/rest/{collection}[?params]`


**Parameters**

Parameter | Description
--------- | -----------
`{mydatabase}` <small>mandatory</small> | Your unique database name, e.g. `sports-xf03`
`{collection}` <small>mandatory</small> | A unique collection name in your database, e.g. `players`
`[params]` <small>optional</small> | See query [parameters](#optional-query-parameters) listed below

### Optional query parameters

Parameter | Default | Description
--------- | ------- | -----------
q | `{}` | Database Query. JSON format
h | `{}` | [Query hints](#query-hints) for Query and output. JSON format
filter | none | Free text search filter
sort | `_id` | Field to sort query result on
dir | `-1` | Sort direction, -1 = ascending, 1 = descending
skip | `0` | Skip forward in result data set
max | `1000` | Data result page size
metafields |  none | Add system fields in data result. See [meta fields](#meta-fields)
totals | none | Return data and paging meta data. See [data result paging](#data-result-paging)
groupby | none | Group data by field
aggregate | none | Aggregate data by field
apikey | none | Add an apikey in as request parameter instead of as a header value (not recommended)
idtolink | none | URLs for links and images
flatten | none | Place deep properies on root object
referencedby | none | refs
fetchmediadata | none | media
fetchchildren | none | child data
format | none | .js or .html

### Query hints

You can add a hint to any query.

```shell
curl -g -X GET \
  'https://{mydatabase}.restdb.io/rest/people?q={"name":"jane"}&h={"$max":20}' \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache' \
  -H 'x-apikey: {MY_API_KEY_HERE}'
```

**Parameters**

Hint | Description
---- | -----------
`$fields` | Show or hide fields in the output data result set. E.g. `h={"$fields":{"title":1, "age": 0}`. Mixing values 0 and 1 are not allowed
`$max` | Max records returnes by query. E.g. `h={"$max": 20}`
`$skip` | Skip records. E.g. `h={"$skip": 100}`
`$orderby` | Sort by field(s). E.g. `h={"$orderby": {"salary": 1, "age": -1}`
`$groupby` | Group data by field(s). E.g. `h={"$groupby":["age", "position"}`. See [aggregation](#aggregation)
`$aggregate` | Aggregate data by expression(s). `h={"$aggregate":["SUM:score"]}`. See [aggregation](#aggregation)


### Meta fields

```shell
curl -X GET \
  https://sports-xf03.restdb.io/rest/companies?&metafields=true \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-apikey: 73bf145c901d1feecf80c26a9d0d1a64aa145'
```
> Example output data with metafields:

```json
[
  {
        "_id": "5631d356f941f47900000110",
        "name": "Nullam Suscipit Est Limited",
        "address": "P.O. Box 460, 4937 Non, Street",
        "city": "La Magdeleine",
        "zip": "AX6 7KK",
        "_keywords": [
            "nullam",
            "suscipit",
            "est",
            "limited",
            "p",
            "o",
            "box",
            "460",
            "4937",
            "non",
            "street",
            "la",
            "magdeleine",
            "ax6",
            "7kk"
        ],
        "_tags": "nullam suscipit est limited p o box 460 4937 non street la magdeleine ax6 7kk",
        "_version": 1,
        "_created": "2015-10-29T08:05:41.947Z",
        "_createdby": "jones@restdb.io"
    }
]
```

Add the metafields URL parameter to get metafields in data result set.


Metafield | Description
---- | -----------
`_id` | Unique document ID
`_keywords` | Array of unique words from the JSON document
`_tags` | Text string of unique words from the JSON document
`_version` | Number inncremented of each update
`_created` | ISO Date string from the document creation time
`_createdby` | Username (email) for the authenticated user that created the document
`_changed` | ISO Date string from the document update time
`_changedby` | Email/username for the authenticated user that changed the document

### Data result paging

```shell
curl -X GET \
  https://sports-xf03.restdb.io/rest/companies?totals=true&skip=10&max=2 \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-apikey: 73bf145c901d1feecf80c26a9d0d1a64aa145'
```

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

For application that needs paging in the result set, use the `?totals=true` query parameter together with `skip` and `max` to retrieve data about totals, page size and page skipping.


## Find a document
Get document by the unique document `_id` from a collection.

**HTTP REQUEST**

> Example code to GET a data item:

```shell
curl -X GET \
  https://sports-xf03.restdb.io/rest/companies/570e052d98290e490000006e \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-apikey: 73bf145c901d1feecf80c26a9d0d1a64aa145'
```

> Example output:

```json
{
    "name": "Jane",
    "status": "amateur",
    "score": 42
}
```

`GET https://{mydatabase}.restdb.io/rest/{collection}/{ID}`


**Parameters**

Parameter | Description
--------- | -----------
`{mydatabase}` <small>mandatory</small> | Your unique database name, e.g. `sports-xf03`
`{collection}` <small>mandatory</small> | A unique collection name in your database, e.g. `players`
`{ID}` <small>mandatory</small> | A unique document ID, e.g. `570e052d98290e490000006e`


## Find a sub document list

**HTTP REQUEST**

`GET	https://{mydatabase}.restdb.io/rest/{mycollection}/{ID}/{my-subcollection}`


## Find a sub document

**HTTP REQUEST**

`GET	https://{mydatabase}.restdb.io/rest/{mycollection}/{ID}/{my-subcollection}/{ID}`

Subcollection is field name of type child and ID is a valid ObjectID.

## Create a new document

**HTTP REQUEST**

`POST	https://{mydatabase}.restdb.io/rest/{mycollection}`

Request body is a valid JSON document.


## Update a document
Update a data item by the unique document `_id` in a collection.

**HTTP REQUEST**

`PUT https://{mydatabase}.restdb.io/rest/{collection}/{ID}`

**Parameters**

Parameter | Description
--------- | -----------
`{mydatabase}` <small>mandatory</small> | Your unique database name, e.g. `sports-xf03`
`{collection}` <small>mandatory</small> | A unique collection name in your database, e.g. `players`
`{ID}` <small>mandatory</small> | A unique document ID, e.g. `570e052d98290e490000006e`
`body` <small>mandatory</small> | Request body, a valid JSON document with properties to update




### Header values
bal bla



## Query language
bla bla

### Logic
bla bla

### Aggregation
bla bla


## Add a new data item to a collection

> Example code to POST a data item:

```shell
curl -X POST \
  https://sports-xf03.restdb.io/rest/companies/570e052d98290e490000006e \
  -H 'Content-Type: application/json' \
  -H 'cache-control: no-cache,no-cache' \
  -H 'x-apikey: 73bf145c901d1feecf80c26a9d0d1a64aa145'
```

```python
def func():
  return
```

> Example output:

```json
{
    "name": "xx",
    "status": "xx",
    "score": 42
}
```

POST a new data item by the to a collection.

**HTTP REQUEST**

`POST https://sports-xf03.restdb.io/rest/companies`

**Parameters**

Parameter | Description
--------- | -----------
`{mydatabase}` <small>mandatory</small> | Your unique database name, e.g. `sports-xf03`
`{collection}` <small>mandatory</small> | A unique collection name in your database, e.g. `players`
`{ID}` <small>mandatory</small> | A unique document ID, e.g. `570e052d98290e490000006e`
`body` <small>mandatory</small> | Request body, a valid JSON document with properties to update


### Data payload
bla bla

### Using POST to emulate PUT, DELETE, PATCH
If your development platform or firewall rules prevent you from calling HTTP methods like PUT, PATCH or DELETE, use the `X-HTTP-Method-Override` header. Pass the method you want to use in the X-HTTP-Method-Override header and make your call using the POST method.




