# Errors

> Error responses include details about what went wrong.

```json
HTTP/1.1 422 Unprocessable Entity
Content-Type: application/vnd.api+json

{
  "errors": [
    {
      "status": "400",
      "source": { "pointer": "/data/attributes/first-name" },
      "title": "Invalid Attribute",
      "detail": "First name must contain at least three characters."
    },
    {
      "status": "400",
      "source": { "pointer": "/data/attributes/first-name" },
      "title": "Invalid Attribute",
      "detail": "First name must contain an emoji."
    }
  ]
}
```
Error responses include details about what went wrong.

**Error Codes**

This list will likely become more comprehensive as features are implemented.

`invalid_params` - The indicated parameters were missing or invalid.    
`unknown_destination` - We weren't able to understand the provided destination, or we don't support it yet. This usually indicates the destination code is wrong, or perhaps not exact enough.    
`request_rate_limit_exceeded` - This API key has made too many requests.    
`account_suspended`    
`not_found`    
`service_unavailable`    
`application_limit_exceeded` - You have hit the maximum amount of ongoing applications allowed.    
`customer_limited` - Your account's limits have been exceeded.    
`agents_busy` - All of our agents are currently busy.    
