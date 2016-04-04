# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: my-api-key"
```

> Make sure to replace `my-api-key` with your API key.

SimpleVisa uses API keys to allow access to the API. You can register a new SimpleVisa API key at our [developer portal](http://simplevisa.com/developers).

SimpleVisa expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: my-api-key`

<aside class="notice">
You must replace <code>my-api-key</code> with your personal API key.
</aside>