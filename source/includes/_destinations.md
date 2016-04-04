# Destinations

## Get All Destinations

```shell
curl "http://example.com/api/destinations"
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

`GET http://api.simplevisa.com/v1/destinations`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include destinations that have already been adopted.

<aside class="success">
Remember — don't forget to authenticate your api call!
</aside>

## Get a Specific Destination

```shell
curl "http://example.com/api/destinations/USA"
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

`GET http://example.com/destinations/<ISO3>`

### URL Parameters

Parameter | Description
--------- | -----------
ISO3 | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the destination to retrieve