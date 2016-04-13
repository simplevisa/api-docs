# Australia

## eVisitor

## ETA

## Get All Authorizations

```shell
curl "http://api.simplevisa.com/v1/authorizations"
  -H "Authorization: my-api-key"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all destinations supported by SimpleVisa.

### HTTP Request

`GET http://api.simplevisa.com/v1/authorizations`

### Query Parameters

Parameter    | Default | Description
------------ | ------- | -------------------------------------------------------------------------------------
include_cats | false   | If set to true, the result will also include cats.
available    | true    | If set to false, the result will include destinations that have already been adopted.

<aside class="success">
Remember — don't forget to authenticate your api call!
</aside>

## Get a Specific Authorization

```shell
curl "http://api.simeplevisa.com/v1/authorizations/XXAARRWWENNNWE"
  -H "Authorization: my-api-key"
```

> The above command returns JSON structured like this:

```json
{
  "id": "USA",
  "name": "United States",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific destination.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://api.simeplevisa.com/v1/authorizations/<authorization>`

### URL Parameters

Parameter     | Description
------------- | -----------------------------------------------------
authorization | The authorization ID of the authorization to retrieve

## Create an Authorization

```shell
curl -X "POST" "http://api.simplevisa.com/v1/authorizations"
  -H "Authorization: my-api-key"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  }
]
```

This endpoint creates an authorization supported by SimpleVisa.

### HTTP Request

`POST http://api.simplevisa.com/v1/authorizations`

### Query Parameters

Parameter    | Default | Description
------------ | ------- | -------------------------------------------------------------------------------------
include_cats | false   | If set to true, the result will also include cats.
available    | true    | If set to false, the result will include destinations that have already been adopted.

<aside class="success">
Remember — don't forget to authenticate your api call!
</aside>
