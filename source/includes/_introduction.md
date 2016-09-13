## Base URL

All URLs referenced in the documentation have the following base:

`https://api.peoplepattern.com`

The People Pattern API is served over HTTPS. To ensure data privacy, unecrypted HTTP is not supported.

## Authentication

HTTP requests to the API are protected with [Token Based authentication](https://www.w3.org/2001/sw/Europe/events/foaf-galway/papers/fp/token_based_authentication/).  This means that you will provide your security token with the Authorization header for authentication.

`curl https://api.peoplepattern.com/enrich \
	
	-H "Authorization: secretkey" `

You can find your security token [on your account page](https://app.peoplepattern.com/edit)

<aside class="notice">
You must replace <code>secretkey</code> with your personal API key.
</aside>
