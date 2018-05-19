# Errors

We highly recommend to log the response body when a response with a HTTP status code >= 400 is returned.

In the case of an error the response will include a human readable error message (see right).

The hate2wait API uses the following error codes.

> Example error message

```shell
{
  "errors": [
    {
      "status": "404",
      "code": "not-found",
      "title": "404 (not found)",
      "detail":"Couldn't find Line with 'id'=1"
    }
  ]
}
```

Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your API key is wrong.
403 | Forbidden -- The kitten requested is hidden for administrators only.
404 | Not Found -- The specified kitten could not be found.
405 | Method Not Allowed -- You tried to access a kitten with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The kitten requested has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're requesting too many kittens! Slow down!
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Please try again later.
