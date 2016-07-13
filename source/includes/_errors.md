# Errors
Capture API uses conventional HTTP response codes to indicate the success or failure of an API request. In general, codes in the <span class="warning">2xx</span> range indicate success, codes in the <span class="warning">4xx</span> range indicate an error that failed given the information provided (e.g., a required parameter was omitted, a charge failed, etc.), and codes in the <span class="warning">5xx</span> range indicate an error with Capture's servers.

Not all errors map cleanly onto HTTP response codes, however. When a request is valid but does not complete successfully, we return a 402 error code.

## Handling errors
Our API libraries raise exceptions for many reasons, such as a failed creation, invalid parameters, authentication errors, and network unavailability. We recommend writing code that gracefully handles all possible API exceptions.

### The Capture API uses the following error codes:

Error Code | Meaning
---------- | -------
400 | Bad Request -- The request was invalid.
401 | Unauthorized -- Your API key is incorrect
402 | Request Failed -- The parameters were valid but the request failed.
403 | Forbidden -- The prospect requested is hidden for administrators only
404 | Not Found -- The specified prospect could not be found
405 | Method Not Allowed -- You tried to access a prospect with an invalid method
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The prospect requested has been removed from our servers
409 | Conflict -- The request conflicts with another request (perhaps due to using the same idempotent key).
429 | Too Many Requests -- You're requesting too many prospects! Slow down!
500, 502, 503, 504 | Server Errors -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.


ATTRIBUTES |
 type | The type of error returned. Can be: api_connection_error, api_error, authentication_error, card_error, invalid_request_error, or rate_limit_error.
 message
 optional | A human-readable message providing more details about the error. For card errors, these messages can be shown to your users.
 code
optional |
For specific errors, a short string from amongst those listed on the right describing the kind of error that occurred.
 param
optional |
The parameter the error relates to if the error is parameter-specific. You can use this to display a message near the correct form field, for example.
