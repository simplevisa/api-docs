# Endpoints

## Get supported programs

> To check supported programs, use this code:

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
          "kind": "VisaWaiver"
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
          "kind": "ElectronicVisa"
        }
      },
      {
        "type": "Program",
        "properties": {
          "name": "ETA",
          "id": "aus-eta",
          "kind": "ElectronicVisa"
        }
      }
    ]
  }
  ...
]
```
Get all supported travel authorization programs supported by SimpleVisa. They can be of different type: Visa Waivers, Electronic Visas, Visas on Arrival, etc.

### HTTP Request
`GET /v1/programs`

## Get program details

> To get a specific program's details , use this code:

```shell
curl -X "GET" "http://api.simplevisa.com/v1/programs/:program_id?nationality=FRA" \
	-H "Authorization: Basic YXNkZmFzZmRhc2RmYWRzYWZzYXNmZDo="
```
> The above command returns JSON structured like this:

```json
[
  {
    "kind": "program_details",
    "program": "usa-vwp",
    "nationality":"FRA",
    "details": {
      "eligible":true,
      "validity":"2 years",
      "features": [
        {
          "type": "Feature",
          "properties": {
            "name": "prepare"
          },
          "params" : [
            {
              "param_name":"usa-vwp_firstname",
              "param_description":"First Name",
              "param_hint":"Traveler's First Name",
              "validations":[
                {
                  "type":"validation",
                  "validation":"less than 90 characters"
                },
                {
                  "type":"validation",
                  "validation":"more than 3 characters"
                }
              ]
            }
          ]
        },
        {
          "type": "Feature",
          "properties": {
            "name": "import"
          },
          "params" : []
        }
      ]

    }
  }
]
```
Get a program's detail to know what's supported (creation, retrieval, check) for each program, and to know what payload (`manifest`) to send when preparing an application.

### HTTP Request
`GET /v1/programs/:program_id?nationality=:nationality`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
nationality | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's main nationality.

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
nationalities | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's nationalities, separated by a comma if multiple nationalities exists.
destination | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's destination country.

## Prepare an application

### HTTP Request
`POST /v1/customers/:customer_id/applications`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
quote_id | The ID of a previously generated delivery quote. Optional, but recommended. Example: "aqt_KSsT9zJdfV3P9k"
manifest | A detailed payload of the application to be processed. See [program details](#get-program-details).
manifest_reference | Optional reference that identifies the manifest. Example: "Customer #690"

## List applications
> you can list all your applications by using this code:

```shell
curl -X "GET" "http://api.simplevisa.com/v1/customers/:customer_id/applications" \
	-H "Authorization: Basic YXNkZmFzZmRhc2RmYWRzYWZzYXNmZDo="
```

> This will result in a response structured like this:

```json
[
  {

  }
]
```
List all applications for a customer.

### HTTP Request
`GET /v1/customers/:customer_id/applications`

## Import an application

> Import an application like this:

```shell
curl -X "POST" "http://api.simplevisa.com/v1/programs/usa-esta" \
	-H "Authorization: Basic YXNkZmFzZmRhc2RmYWRzYWZzYXNmZDo=" \
	-H "Content-Type: application/x-www-form-urlencoded" \
    --data-urlencode "program_id=usa-vwp"
  	--data-urlencode "manifest={\"data\"=\"data\"}" \
```

> This will give you the result like this, or an error if the application was not found.

```json
[
  {
    "sdds":"sdds"
  }
]
```

It is possible to import existing applications into your account, if the country's program allows it (see [program's details](#get-program-details) to check ). This endpoint allows you to check for an existing travel authorization or retrieve a lost one on the country's program system.

### HTTP Request
`POST /v1/customers/:customer_id/applications/import`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
program_id | The program Id of the application to import
manifest | The payload to import a document based on the program's details

## Get an application

Retrieve updated details about an application.

### HTTP Request
`GET /v1/customers/:customer_id/applications/:application_id`
