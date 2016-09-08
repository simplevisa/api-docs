---
title: SimpleVisa API Reference

language_tabs:
  - shell

toc_footers:
  - <a href='http://simplevisa.com/developers'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>

includes:
  - endpoints
  - errors
  - resources

search: true
---

# Overview

Welcome to the SimpleVisa API! You can use our API to access SimpleVisa API endpoints.

To get started using the SimpleVisa API:

- Sign up for a [developer account](http://simplevisa.com/developers).
- Describe your app or idea in details to get approved for an API key. See [Approval Guidelines](#approval-guidelines)
- Locate your `project ID` and `API key` in the developer dashboard.

## What can the API do?

You can use the SimpleVisa API to create travel authorizations for supported destinations.

Here is the flow of events that developers most commonly follow when using our API:

- To see if an authorization is possible, request an [application quote & eligibility](#get-requirements-and-quote). This endpoint takes in a destination country and one or more citizenship country and returns a fee, ETA, and other information about a potential authorization.
- After you have evaluated whether the quoted price and authorization estimate meets your needs, you need to get the [program details](#get-program-details)
- You can then [prepare an application](#prepare-an-application) with the details obtained in previous API call.
- While an authorization is in progress, you can track its status in real-time in the developer dashboard, by polling the API, or with webhooks.

## Requests

The base URL for all requests to the SimpleVisa API is:

`https://api.simplevisa.com/`

Our API is REST-based. This means:

- It make use of standard HTTP verbs like GET, POST, DELETE.
- The API uses standard HTTP error responses to describe errors.
- Authentication is specified with HTTP Basic Authentication. All requests use standard query encoding.

POST data should be encoded as standard `application/x-www-form-urlencoded`.

<!-- ## Versioning

Versioning allows us to provide developers a consistent experience. We provide two levels of versioning:

- Resource: All endpoints are prefixed with a version such as `/v1`. This version refers to the overall layout of the endpoints and response standards.
- Client: Developers can ensure consistent fields and formats by specifying a version as a HTTP header. `X-Simplevisa-Version` header such as `X-Simplevisa-Version: 20160403` -->

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.simplevisa.com/v1"
  -H "x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55"
```

> Make sure to replace the demo key with your API key.

The SimpleVisa API requires authentication by API key. You can register a new SimpleVisa API key at our [developer portal](http://simplevisa.com/developers).

The actual header that is used will be a base64-encoded string like this:

`x-api-key: bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55`

<aside class="notice">
You must replace <code>bkayZOMvuy8aZOhIgxq94K9Oe7Y70Hw55</code> with your own personal API key.
</aside>

Most of the [endpoints](#endpoints) provided in the SimpleVisa API are in relation to a specific project. You'll need to provide your **project id** and include it in the URL.
