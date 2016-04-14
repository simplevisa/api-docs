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

search: true
---

<aside class="success">
This documentation is a work in progress.
</aside>

# Overview

Welcome to the SimpleVisa API! You can use our API to access SimpleVisa API endpoints.

To get started using the SimpleVisa API:

- Sign up for a [developer account](http://simplevisa.com/developers).
- Locate your `customer ID` and `test API key` in the developer dashboard.

## What can the API do?

You can use the SimpleVisa API to create travel authorizations for supported destinations.

Here is the flow of events that developers most commonly follow when using our API:

- To see if an authorization is possible, request an [application quote](#get-requirements-and-quote). This endpoint takes in two countries and returns a fee, ETA, and other information about a potential authorization.
- After you have evaluated whether the quoted price and authorization estimate meets your needs, you can [prepare an application](#prepare-an-application).
- While an authorization is in progress, you can track its status in real-time in the developer dashboard, by polling the API, or with webhooks.

## Requests

The base URL for all requests to the SimpleVisa API is:

`https://api.simplevisa.com/`

Our API is REST-based. This means:

- It make use of standard HTTP verbs like GET, POST, DELETE.
- The API uses standard HTTP error responses to describe errors.
- Authentication is specified with HTTP Basic Authentication. All requests use standard query encoding.

POST data should be encoded as standard `application/x-www-form-urlencoded`.

## Versioning

Versioning allows us to provide developers a consistent experience. We provide two levels of versioning:

- Resource: All endpoints are prefixed with a version such as `/v1`. This version refers to the overall layout of the endpoints and response standards.
- Client: Developers can ensure consistent fields and formats by specifying a version as a HTTP header. `X-Simplevisa-Version` header such as `X-Simplevisa-Version: 20160403`

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "https://api.simplevisa.com/v1"
  -H "Authorization: Basic ZmdoZ2pmamhnZjoqKioqKiBIaWRkZW4gY3JlZGVudGlhbHMgKioqKio="
```

> Make sure to replace the demo key with your API key.

The SimpleVisa API requires authentication by [HTTP Basic Auth](http://en.wikipedia.org/wiki/Basic_access_authentication) headers. You can register a new SimpleVisa API key at our [developer portal](http://simplevisa.com/developers). Your API key should be included as the username. The password should be left empty.

The actual header that is used will be a base64-encoded string like this:

`Authorization: Basic Y2YyZjJkNmQtYTMxNC00NGE4LWI2MDAtNTA1M2MwYWYzMTY1Og==`

<aside class="notice">
You must replace <code>Y2YyZjJkNmQtYTMxNC00NGE4LWI2MDAtNTA1M2MwYWYzMTY1Og==</code> with your own authentication based on your personal API key.
</aside>

Most of the [endpoints](#endpoints) provided in the SimpleVisa API are in relation to a specific customer. You'll need to provide your **customer id** and include it in the URL.
