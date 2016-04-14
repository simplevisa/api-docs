# Endpoints

## Get supported programs

```shell
curl -X "GET" "http://api.simplevisa.com/v1/programs"
  -H "Authorization: my-api-key"
```

> The above command returns JSON structured like this:

```json
[
  {
    "type": "ProgramsCollection",
    "properties": {
      "zone_name": "United States",
      "market_name": "United States"
    },
    "programs": [
      {
        "type": "Program",
        "properties": {
          "name": "VWP",
          "id": "usa-vwp",
          "type": "VisaWaiver"
        }
      }
    ]
  },
  {
    "type": "ProgramsCollection",
    "properties": {
      "zone_name": "Australia",
      "market_name": "Australia"
    },
    "programs": [
      {
        "type": "Program",
        "properties": {
          "name": "eVisitors",
          "id": "aus-evisitors",
          "type": "ElectronicVisa"
        }
      },
      {
        "type": "Program",
        "properties": {
          "name": "ETA",
          "id": "aus-eta",
          "type": "ElectronicVisa"
        }
      }
    ]
  }
  ...
]
```

### HTTP Request
`GET /v1/programs`

## Get program details

### HTTP Request
`GET /v1/programs/:program_id`

## Get requirements and quote

```shell
curl -X "POST" "http://api.simplevisa.com/v1/customers/:customer_id/application_quotes" \
	-H "Authorization: Basic YXNkZmFzZmRhc2RmYWRzYWZzYXNmZDo=" \
	-H "Content-Type: application/x-www-form-urlencoded" \
	--data-urlencode "destination=USA" \
	--data-urlencode "nationalities=FRA,DEU"
```

> The above command returns JSON structured like this:

```json
[
  {
    "kind": "application_quote",
    "id": "aqt_qUdje83jhdk",
    "created": "2014-04-13T10:04:03Z",
    "expires": "2014-04-13T10:09:03Z",
    "program": "usa-vwp",
    "main_nationality_used": "FRA",
    "fee": 1400,
    "currency": "usd",
    "credits": 1820,
    "processing_eta": "2014-04-13T10:12:03Z",
    "duration": 3
  },
  {
    "kind": "application_quote",
    "id": "aqt_qUdje83hfyt",
    "created": "2014-04-13T10:04:03Z",
    "expires": "2014-04-13T10:09:03Z",
    "program": "usa-vwp",
    "main_nationality_used": "DEU",
    "fee": 1400,
    "currency": "usd",
    "credits": 1820,
    "processing_eta": "2014-04-13T10:12:03Z",
    "duration": 3
  }
]
```

### HTTP Request
`POST /v1/customers/:customer_id/application_quotes`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
nationalities | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's nationalities, separated by a comma.
destination | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's destination country.

## Prepare an application

### HTTP Request
`POST /v1/customers/:customer_id/applications`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
authorization | The authorization ID of the authorization to retrieve

## List applications

### HTTP Request
`GET /v1/customers/:customer_id/applications`

## Import an application

### HTTP Request
`POST /v1/customers/:customer_id/applications/import`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
authorization | The authorization ID of the authorization to retrieve

## Get an application

### HTTP Request
`GET /v1/customers/:customer_id/applications/:application_id`
