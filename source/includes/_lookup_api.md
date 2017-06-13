# Lookup API

The Lookup API provides access to the Portrait database (PDB) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  
This endpoint supports both HTTP POST and HTTP GET calls.


## Profile Lookup

Retrieve one or more profiles from the PDB by submitting their relevant social profile identifiers.  If found, an enriched profile (referred to as a portrait) will be returned.

Lookup supports the following services:

- `foursquare`
- `googleplus`
- `instagram`
- `tumblr`
- `twitter`
- `youtube`

To restrict results to just one or just several services, only request ids with an appropriate prefix:

  twitter:12345
  instagram:56789

When looking up a batch of profiles the response will include each submitted social platform identifier, if a profile is not found in the PDB it is left out of the response.

### Resource URI

`/lookup`

### Json Schema

type                  | schema URL
----------------------|-----------
Lookup Request        | [http://apidocs.peoplepattern.com/schemata/LookupRequest.json](http://apidocs.peoplepattern.com/schemata/LookupRequest.json)
Lookup Response        | [http://apidocs.peoplepattern.com/schemata/LookupResponse.json](http://apidocs.peoplepattern.com/schemata/LookupResponse.json)

### GET example

```shell
curl "https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN&id=twitter:14132201,twitter:119837224&fields=handle" \
  -H "Accept: application/json"
```

```json
{
  "twitter:14132201": {
    "name": "chonuff"
  },
  "twitter:119837224": {
    "name": "jasonbaldridge"
  }
}
```

### POST example

```
curl "https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN" \
  -X POST \
  -H "Accept: application/json" \
  -d '{"fields": ["name"],"ids": ["twitter:14132201","twitter:119837224"]}'
```

```
{
  "twitter:14132201": {
    "name": "Kenneth Cho"
  },
  "twitter:119837224": {
    "name": "Jason Baldridge"
  }
}
```
