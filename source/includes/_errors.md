# Errors

The People Pattern API uses the following error codes:


Error Code | Meaning
---------- | -------
400 | Bad Request -- Malformed request
401 | Unauthorized -- Your API key is wrong
404 | Not Found -- The requested resource is not available on the API
406 | Not Acceptable -- You requested a format that isn't json
410 | Gone -- The resource requested has been removed from our servers
429 | Too Many Requests -- Too many concurrent requests are being made by your client
500 | Internal Server Error -- Service side error -- please contact us a <api-help@peoplepattern.com>
503 | Service Unavailable -- Service is offline for maintenance