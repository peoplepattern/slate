# Enrich API

The Enrich API enables you to access the predictions of our
profile and text models to extract personal attributes, like
demographics and location information, from standard
semistructured profile data structures.

### Why you might need the Enrich API

Similar functionality is provided by the [Lookup API](#lookup-api)
provided you have social profile IDs or screen names. For many
users, IDs or screen names are more easily acquired (e.g. off of
CRMs or user databases) than full profile content, which usually
must be fetched from a social network API.

This API fills some gaps in Lookup API functionality:

- Our PDB is largely (though not entirely) comprised of Twitter
  data, so for social network data from other resources your
  application may have access to -- Reddit profile data, for
  example -- you can enrich this data with the Enrich API.
- We've collected a large number of Twitter profiles in the PDB,
  but do not guarantee total coverage. Moreover, as users change
  their screen names often, we can not guarantee being able to
  find a user by an outdated screen name, or one which has been
  very recently changed
- The Enrich API gives you textual enrichments on individual
  texts (i.e. social media posts), for **sentiment**,
  **language** and **interests** attributes. The PDB access
  APIs only provide access to profile attributes.

### Enrich API philosophy

This API enriches your content; for this reason, it takes as
input fairly arbitrary data serialized as JSON, and echoes that
content back in the response only with predicted enrichments. This
allows the client to, for instance, include an identifier which may
be used to retrieve the record from a database to update with
People Pattern enrichments; by including these details in the
API response body, the client does not need to keep track of
which records in single or batch responses correspond with which
inputs.

## Enrich a single profile

```http
POST /enrich/profile HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey

{"name":"Joe User", "username": "juser", "description": "my profile", "location": "Boston, USA"}
```

```shell
curl https://api.peoplepattern.com/enrich/profile \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"name":"Joe User", "username": "juser", "description": "my profile", "location": "Boston, USA"}'
```

> Response will look like:

```shell
{"name":"Joe User","username":"juser","description":"my profile","location":"Boston, USA","peoplepattern":{"account_type":"person" ....
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-Request-Id: 9372aa09-eb86-4366-889e-02a1a5107432

{"name":"Joe User","username":"juser","description":"my profile","location":"Boston, USA","peoplepattern":{"account_type":"person" ....
```

When passing a single [profile](#profile-input) to the
enrich profile endpoint, the profile data structure is passed
back to the client with a `peoplepattern` field filled with
[profile enrichments](#profile-enrichments).

<aside class="notice">
We use the HTTP POST method, since some clients do not allow you to
send request bodies with HTTP requests. For some requests, especially
<a href="#enrich-a-profile-batch">the profile batch call</a>, we want
to ensure the API supports JSON request bodies.
</aside>

<aside class="notice">
The Enrich API also supports document formats provided by social media
API, starting with the Twitter API. By passing a
<a href="https://dev.twitter.com/overview/api/users">Twitter user object</a> in the
Twitter standard API JSON format, the Enrich API will return the document
in its original format only with a new "peoplepattern" field, populated
as above.
</aside>

## Enrich a profile batch

```http
POST /enrich/profile HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey

[{"name":"Joe User", "username": "juser", "description": "my profile", "location": "Boston, USA"}, {"name": "Mary Brown", "username": "mbrown", "description": "This is Mary's profile"}]
```

```shell
curl https://api.peoplepattern.com/enrich/profile \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '[{"name":"Joe User", "username": "juser", "description": "my profile", "location": "Boston, USA"}, {"name": "Mary Brown", "username": "mbrown", "description": "This is Marys profile"}]'
```

> Response will look like:

```shell
[{"status":"success","code":200,"response":{"account_type":"person","spam":false,"adult":false,"vcard":{"name":{"given-name":"Joe","family-name":"User","fn":"Joe User"},"email":[]},"demographics":{"birthyear":1985,"gender":"male","race":"white"},"place":{"city":true,"geo_name_id":4930956,"type":"City","location":{"dma":"Boston, MA-Manchester, NH","city":"Boston","state":"Massachusetts","state_abbreviation":"MA","utc_offset":"-18000","time_zone":"America/New_York","metro_area":"Boston-Cambridge-Newton, MA-NH","continent":"NA","language":"en","population":617594,"place_type":"City","country":"United States","country_code":"US","coordinates":{"longitude":42.35843,"latitude":-71.05977}}}}]
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-Request-Id: 9372aa09-eb86-4366-889e-02a1a5107432

[{"status":"success","code":200,"response":{"account_type":"person","spam":false,"adult":false,"vcard":{"name":{"given-name":"Joe","family-name":"User","fn":"Joe User"},"email":[]},"demographics":{"birthyear":1985,"gender":"male","race":"white"},"place":{"city":true,"geo_name_id":4930956,"type":"City","location":{"dma":"Boston, MA-Manchester, NH","city":"Boston","state":"Massachusetts","state_abbreviation":"MA","utc_offset":"-18000","time_zone":"America/New_York","metro_area":"Boston-Cambridge-Newton, MA-NH","continent":"NA","language":"en","population":617594,"place_type":"City","country":"United States","country_code":"US","coordinates":{"longitude":42.35843,"latitude":-71.05977}}}}]
```

> Example invalid format call with output

```shell
curl https://api.peoplepattern.com/enrich/profile \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '[{}]'

[{"status":"error","code":400,"error":{"input":{},"message":"No valid fields provided for profile content"}}]
```

```http
POST /enrich/profile HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey

[{}]
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-Request-Id: 9372aa09-eb86-4366-889e-02a1a5107432

[{"status":"error","code":400,"error":{"input":{},"message":"No valid fields provided for profile content"}}]
```

When passing a batch of profiles to the enrich profile endpoint,
the client receives a batch of responses. Since each profile request
may succeed or fail individually, the batch of responses included
their own meta-data with respect to the response status.

<aside class="notice">
As with the single-profile call, batches of Twitter API format "users"
are also supported.
</aside>

## Enrich a social media post

```shell
curl https://api.peoplepattern.com/enrich/post \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"text":"Bowling tonight? or kung-fu?"}'
```

```http
POST /enrich/post HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey

{"text":"Bowling tonight? or kung-fu?"}
```

> Response will look like:

```shell
{"text":"Bowling tonight? or kung-fu?","peoplepattern":{"interests":["leisure_sports"],"languages":["en"],"sentiment":"neutral","interestingness":0.7085509373685894}}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-Request-Id: 80990215-d2f5-4dbd-836c-9bb3f3613539

{"text":"Bowling tonight? or kung-fu?","peoplepattern":{"interests":["leisure_sports"],"languages":["en"],"sentiment":"neutral","interestingness":0.7085509373685894}}
```

When passing a single [post](#post-input) to the
enrich post endpoint, the post data structure is passed
back to the client with a `peoplepattern` field filled with
[post enrichments](#post-enrichments).

<aside class="notice">
Since the Twitter API standard <a href="https://dev.twitter.com/overview/api/tweets">tweet</a>
data structures do contain a "text" field, the Enrich API
social media post enrichment call will work with tweet JSON
</aside>

## Enrich a post batch

```shell
curl https://api.peoplepattern.com/enrich/post \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '[{"text":"Bowling tonight? or kung-fu?"},{"text":"I love bowling with friends"},{"text":"But I also love eating at home with the family"}]'
```

```http
POST /enrich/post HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey

[{"text":"Bowling tonight? or kung-fu?"},{"text":"I love bowling with friends"},{"text":"But I also love eating at home with the family"}]
```

> Response will look like:

```shell
[{"status":"success","code":200,"result":{"text":"Bowling tonight? or kung-fu?","peoplepattern":{"interests":["leisure_sports"],"languages":["en"],"sentiment":"neutral","interestingness":0.7085509373685894}}},{"status":"success","code":200,"result":{"text":"I love bowling with friends","peoplepattern":{"interests":["leisure_sports"],"languages":["en"],"sentiment":"positive","interestingness":0.5522605037296693}}},{"status":"success","code":200,"result":{"text":"But I also love eating at home with the family","peoplepattern":{"interests":["family"],"languages":["en"],"sentiment":"positive","interestingness":0.5893891902193789}}}]
```

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
X-Request-Id: 80990215-d2f5-4dbd-836c-9bb3f3613539

[{"status":"success","code":200,"result":{"text":"Bowling tonight? or kung-fu?","peoplepattern":{"interests":["leisure_sports"],"languages":["en"],"sentiment":"neutral","interestingness":0.7085509373685894}}},{"status":"success","code":200,"result":{"text":"I love bowling with friends","peoplepattern":{"interests":["leisure_sports"],"languages":["en"],"sentiment":"positive","interestingness":0.5522605037296693}}},{"status":"success","code":200,"result":{"text":"But I also love eating at home with the family","peoplepattern":{"interests":["family"],"languages":["en"],"sentiment":"positive","interestingness":0.5893891902193789}}}]
```

When passing a batch of posts to the enrich post endpoint,
the client receives a batch of responses. Since each post request
may succeed or fail individually, the batch of responses included
their own meta-data with respect to the response status.

<aside class="notice">
As with the single-post call, batches of Twitter API format "tweets"
are also supported.
</aside>