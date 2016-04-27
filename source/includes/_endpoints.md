# Endpoints

## Get supported programs

> To check supported programs, use this code:

```shell
curl -X "GET" "http://api.simplevisa.com/programs"
  -H "x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55"
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
Get all supported travel authorization programs supported by SimpleVisa. One country can have mulitple programs available depending on preference or traveler's nationality. They can also be of different type: Visa Waivers, Electronic Visas, Visas on Arrival, etc.

### HTTP Request
`GET /programs`

## Get requirements and quote

```shell
curl -X "POST" "http://api.simplevisa.com/projects/:project_id/application_quotes" \
	-H "x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55" \
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
`POST /projects/:project_id/application_quotes`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
nationalities | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's nationalities, separated by a comma if multiple nationalities exists.
destination | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's destination country.

## Get program details

> To get a specific program's details , use this code:

```shell
curl -X "GET" "http://api.simplevisa.com/programs/:program_id?nationality=FRA" \
	-H "x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55"
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
`GET /programs/:program_id?nationality=:nationality`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
nationality | The [ISO 3166-1 alpha-3](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) code of the traveler's main nationality.

## List applications
> you can list all your applications by using this code:

```shell
curl -X "GET" "http://api.simplevisa.com/projects/:project_id/applications" \
	-H "x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55"
```

> This will result in a response structured like this:

```json
{
    "code": 200,
    "status": "ok",
    "messages": [],
    "result": {
        "user": {
            "id": 123,
            "name": "test"
        }
    }
}
```
List all applications for a customer.

pagination

### HTTP Request
`GET /projects/:project_id/applications`

## Prepare an application

### HTTP Request
`POST /projects/:project_id/applications`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
quote_id | The ID of a previously generated delivery quote. Optional, but recommended. Example: "aqt_KSsT9zJdfV3P9k"
manifest | A detailed payload of the application to be processed. See [program details](#get-program-details).
manifest_reference | Optional reference that identifies the manifest. Example: "Customer #690"

## Import an application

> Import an application like this:

```shell
curl -X "POST" "http://api.simplevisa.com/programs/usa-esta" \
	-H "x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55" \
	-H "Content-Type: application/x-www-form-urlencoded" \
    --data-urlencode "program_id=usa-vwp"
  	--data-urlencode "manifest={\"data\"=\"data\"}" \
```

> This will give you the result like this, or an error if the application was not found.

```json
{
    "code": 200,
    "status": "ok",
    "messages": [],
    "result": {
        "user": {
            "id": 123,
            "name": "test"
        }
    }
}
```

It is possible to import existing applications into your account, if the country's program allows it (see [program's details](#get-program-details) to check ). This endpoint allows you to check for an existing travel authorization or retrieve a lost one on the country's program system.

### HTTP Request
`POST /projects/:project_id/applications/import`

### Query Parameters

Parameter     | Description
------------- | -----------------------------------------------------
program_id | The program Id of the application to import
manifest | The payload to import a document based on the program's details

## Get an application

Retrieve updated details about an application.

### HTTP Request
`GET /projects/:project_id/applications/:application_id`
