# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Basic ZmdoZ2pmamhnZjoqKioqKiBIaWRkZW4gY3JlZGVudGlhbHMgKioqKio="
```

> Make sure to replace `my-api-key` with your API key.

SimpleVisa uses API keys to allow access to the API. You can register a new SimpleVisa API key at our [developer portal](http://simplevisa.com/developers).

SimpleVisa expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: my-api-key`

<aside class="notice">
You must replace <code>my-api-key</code> with your personal API key.
</aside>

The SimpleVisa API requires authentication by [HTTP Basic Auth](http://en.wikipedia.org/wiki/Basic_access_authentication) headers. Your API key should be included as the username. The password should be left empty.

The actual header that is used will be a base64-encoded string like this:

`Basic Y2YyZjJkNmQtYTMxNC00NGE4LWI2MDAtNTA1M2MwYWYzMTY1Og==`

Most of the [endpoints](http://) provided in the SimpleVisa API are in relation to a specific customer. You'll need to provide your customer id and include it in the URL.