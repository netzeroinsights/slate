# Errors

The Net Zero Insights API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your credentials are wrong.
402 | You have reached the maximum number of searches allowed for your subscription.
403 | Forbidden -- The requested resource is hidden for administrators only.
404 | Not Found -- The specified resource could not be found.
405 | Method Not Allowed -- You tried to access a resource with an invalid method.
406 | Not Acceptable -- You requested a format that isn't json.
410 | Gone -- The requested resource has been removed from our servers.
418 | I'm a teapot.
429 | Too Many Requests -- You're requesting too many resource. Try again later
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarily offline for maintenance. Try again later.
