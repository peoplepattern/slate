## Base URL

All URLs referenced in the documentation have the following base:

`https://api.peoplepattern.com`

The People Pattern API is served over HTTPS. To ensure data privacy, unencrypted HTTP is not supported.

All calls require a Content-Type header.

If you're POSTing json, use:

`Content-Type: application/json`

If you're POSTing hocon, use:

`Content-Type: application/hocon`

## Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the access token as a url parameter with each request
curl https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN

```

> Make sure to replace `$MY_TOKEN` with your API access token.

HTTP requests to the API are protected with [Token Based authentication](https://www.w3.org/2001/sw/Europe/events/foaf-galway/papers/fp/token_based_authentication/).  The People Pattern API expects the API security token to be included in all API requests to the server as a url parameter that looks like the following:

`access_token=$MY_TOKEN`

You can find your security token [on your account page](https://app.peoplepattern.com/edit).

<aside class="notice">
You must replace <code>$MY_TOKEN</code> with your personal API security token.
</aside>
