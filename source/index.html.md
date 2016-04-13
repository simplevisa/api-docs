---
title: API Reference
language_tabs:
  - shell
toc_footers:
  - "<a href='http://simplevisa.com/developers'>Sign Up for a Developer Key</a>"
  - "<a href='https://github.com/tripit/slate'>Documentation Powered by Slate</a>"
includes:
  - authentication
  - destinations
  - usa
  - tur
  - can
  - errors
search: true
---

<aside class="success">
This documentation is a work in progress.
</aside>

# Overview

Welcome to the SimpleVisa API! You can use our API to access SimpleVisa API endpoints.

To get started using the SimpleVisa API:

- Sign up for a developer account.
- Locate your customer ID and test API key in the developer dashboard.
- Check out a few tutorials on how to use the API: [cURL](http://), [Postman](http://).

## What can the API do?

You can use the SimpleVisa API to create travel authorizations for supported destinations.

Here is the flow of events that developers most commonly follow when using our API:

- To see if an authorization is possible, request a [authorization quote](http://). This endpoint takes in two countries and returns a fee, ETA, and other information about a potential authorization.
- After you have evaluated whether the quoted price and authorization estimate meets your needs, you can [create an authorization](http://).
- While an authorization is in progress, you can track its status in real-time in the developer dashboard, by [polling the API](http://), or with [webhooks](http://).

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
