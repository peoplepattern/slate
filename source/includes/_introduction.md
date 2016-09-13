## Base URL

All URLs referenced in the documentation have the following base:

`https://api.peoplepattern.com`

The People Pattern API is served over HTTPS. To ensure data privacy, unecrypted HTTP is not supported.

All calls require a Content-Type header

`Content-type: application/json`

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl https://api.peoplepattern.com/... \
  -H "Authorization: securitytoken"
```

> Make sure to replace `securitytoken` with your API security token.

HTTP requests to the API are protected with [Token Based authentication](https://www.w3.org/2001/sw/Europe/events/foaf-galway/papers/fp/token_based_authentication/).  The People Pattern API expected for the API security token to be included in all API requests to the server in a header that looks like the following:

`Authorization: securitytoken`

You can find your security token [on your account page](https://app.peoplepattern.com/edit).

<aside class="notice">
You must replace <code>securitytoken</code> with your personal API security token.
</aside>
