# Enrich API

The Enrich API provides access to our audience intelligence
and machine-learned based models used to extract personal attributes,
like demographics and location information from profile and post data.

This API takes as input a serialized as JSON object, and echoes that
content back in the response along with predicted enrichments. This
allows you to include an identifier which gets returned in the response and may
be used as a reference id.

## Profile Enrich

When enriching a profile the profile data structure is passed back to the client along with the profile enrichments.

### Resource URI enrich-profile

`/profile`

### HTTP POST
To enrich a profile, make an HTTP POST request to [Profile Enrich endpoint](#resource-uri-enrich-profile).  
We use the HTTP POST method, since some clients do not allow you to
send request bodies with HTTP GET requests.

#### POST PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|------------
`body`        | Yes      | a [profile object](#profile-input) or an array of profile objects

<aside class="notice">
The Enrich API also supports document formats provided by social media
API, starting with the Twitter API. By passing a
<a href="https://dev.twitter.com/overview/api/users">Twitter user object</a> in the
Twitter standard API JSON format, the Enrich API will return the document
in its original format only with a new "peoplepattern" field, populated
as above.
</aside>

### Enrich a single profile

```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/profile" \
  -d '{"name":"Joe User", "username": "juser", "description": "my profile", "location": "Boston, USA"}'
```

TODO: rerun this, response format out of date

```json
{
  "name": "Joe User",
  "username": "juser",
  "description": "my profile",
  "location": "Boston, USA",
  "peoplepattern": {
    "account_type": "person",
    "spam": false,
    "adult": false,
    "vcard": {
      "name": {
        "given-name": "Joe",
        "family-name": "User",
        "fn": "Joe User"
      },
      "email": []
    },
    "demographics": {
      "birthyear": 1985,
      "gender": "male",
      "race": "white"
    },
    "place": {
      "name": "Boston, Massachusetts",
      "city": true,
      "geo_name_id": 4930956,
      "type": "City",
      "location": {
        "dma": "Boston, MA-Manchester, NH",
        "city": "Boston",
        "state": "Massachusetts",
        "state_abbreviation": "MA",
        "utc_offset": "-18000",
        "time_zone": "America/New_York",
        "metro_area": "Boston-Cambridge-Newton, MA-NH",
        "continent": "NA",
        "language": "en",
        "population": 617594,
        "place_type": "City",
        "country": "United States",
        "country_code": "US",
        "coordinates": {
          "longitude": 42.35843,
          "latitude": -71.05977
        }
      }
    },
    "extended_demographics": {},
    "interestingness": 0.8431624560581947,
    "_meta": {
      "source": "current-models",
      "model_version": "0.11-pre4",
      "predict_fields": [
        "name",
        "username",
        "description",
        "location"
      ]
    }
  }
}
```

When passing a single [profile](#profile-input) to the
enrich profile endpoint, the profile data structure is passed
back to the client with a `peoplepattern` field filled with
[profile enrichments](#profile-enrichments).

### Enrich a batch of profiles

```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/profile" \
  -d '[{"name":"Joe User", "username": "juser", "description": "my profile", "location": "Boston, USA"}, {"name": "Mary Brown", "username": "mbrown", "description": "This is Marys profile"}]'
```

```json
[
  {
    "status": "success",
    "code": 200,
    "result": {
      "name": "Joe User",
      "username": "juser",
      "description": "my profile",
      "location": "Boston, USA",
      "peoplepattern": {
        "account_type": "person",
        "spam": false,
        "adult": false,
        "vcard": {
          "name": {
            "given-name": "Joe",
            "family-name": "User",
            "fn": "Joe User"
          },
          "email": []
        },
        "demographics": {
          "birthyear": 1985,
          "gender": "male",
          "race": "white"
        },
        "place": {
          "name": "Boston, Massachusetts",
          "city": true,
          "geo_name_id": 4930956,
          "type": "City",
          "location": {
            "dma": "Boston, MA-Manchester, NH",
            "city": "Boston",
            "state": "Massachusetts",
            "state_abbreviation": "MA",
            "utc_offset": "-18000",
            "time_zone": "America/New_York",
            "metro_area": "Boston-Cambridge-Newton, MA-NH",
            "continent": "NA",
            "language": "en",
            "population": 617594,
            "place_type": "City",
            "country": "United States",
            "country_code": "US",
            "coordinates": {
              "longitude": 42.35843,
              "latitude": -71.05977
            }
          }
        },
        "extended_demographics": {},
        "interestingness": 0.8431624560581947,
        "_meta": {
          "source": "current-models",
          "model_version": "0.11-pre4",
          "predict_fields": [
            "name",
            "username",
            "description",
            "location"
          ]
        }
      }
    }
  },
  {
    "status": "success",
    "code": 200,
    "result": {
      "name": "Mary Brown",
      "username": "mbrown",
      "description": "This is Mary's profile",
      "peoplepattern": {
        "account_type": "person",
        "spam": false,
        "adult": false,
        "vcard": {
          "name": {
            "given-name": "Mary",
            "family-name": "Brown",
            "fn": "Mary Brown"
          },
          "email": []
        },
        "demographics": {
          "birthyear": 1962,
          "gender": "female",
          "race": "white"
        },
        "extended_demographics": {},
        "interestingness": 0.9613207296903373,
        "_meta": {
          "source": "current-models",
          "model_version": "0.11-pre4",
          "predict_fields": [
            "name",
            "username",
            "description"
          ]
        }
      }
    }
  }
]
```

When passing a batch of profiles to the enrich profile endpoint,
the client receives a batch of responses. Since each profile request
may succeed or fail individually, the batch of responses included
their own meta-data with respect to the response status.

<aside class="notice">
As with the single-profile call, batches of Twitter API format "users"
are also supported.
</aside>

### Error Sample

To see a comprehensive list of error status returned the the People Pattern Audience Intelligence API please see the [Errors section](#errors).  
Here we have displayed what a same error response would look like from the Enrich API.

> Example invalid format call with output

```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/profile" \
  -d '[{}]'

[{"status":"error","code":400,"error":{"input":{},"message":"No valid fields provided for profile content"}}]
```

## Post Enrich

When enriching a post the post data structure is passed back to the client along with the profile enrichments.

### Resource URI enrich-post

`/post`

### HTTP POST
To enrich a post, make an HTTP POST request to [Post Enrich endpoint](#resource-uri-enrich-post).  
We use the HTTP POST method, since some clients do not allow you to
send request bodies with HTTP GET requests.

#### POST PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`body`        | Yes      | a [post object](#post-input) or a array of post objects

<aside class="notice">
Similar to the Twitter API's <a href="https://dev.twitter.com/overview/api/tweets">tweet</a>
data structures which contain a "text" field, the Enrich API
social media post enrichment call will work with the same tweet JSON
</aside>

## Post (input)

A social media post or other text may be passed to the Enrich API
as a JSON object with a string-valued `text` field

field      | type
-----------|------
text       | string

JSON objects containing other fields may be used, and other
fields are provided back to the client in
[enriched post output](#enriched-post)

## Post enrichments

> Sample post enrichments as JSON

```json
{
  "interests": [
    "science"
  ],
  "languages": [
    "en"
  ],
  "sentiment": "neutral"
}
```

Post enrichments consist of a set of predicted interest topics,
predicted languages and predicted sentiment

field           | type            | description
----------------|-----------------|-----------------------------------------
interests       | array of string | [interest topics](#interest-topic-values)
languages       | array of string | [ISO 639-1 two letter language codes](https://en.wikipedia.org/wiki/ISO_639-1)
sentiment       | string          | "positive", "negative" or "neutral"

### Enrich a single post

```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/post" \
  -d '{"text":"Bowling tonight? or kung-fu?"}'
```

```json
{
  "text": "Bowling tonight? or kung-fu?",
  "peoplepattern": {
    "interests": [
      "leisure_sports"
    ],
    "languages": [
      "en"
    ],
    "sentiment": "neutral",
    "interestingness": 0.7085509373685894
  }
}
```

When passing a single [post](#post-input) to the
enrich post endpoint, the post data structure is passed
back to the client with a `peoplepattern` field filled with
[post enrichments](#post-enrichments).


### Enrich a batch of posts

```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/post" \
  -d '[{"text":"Bowling tonight? or kung-fu?"},{"text":"I love bowling with friends"},{"text":"But I also love eating at home with the family"}]'
```

```json
[
  {
    "status": "success",
    "code": 200,
    "result": {
      "text": "Bowling tonight? or kung-fu?",
      "peoplepattern": {
        "interests": [
          "leisure_sports"
        ],
        "languages": [
          "en"
        ],
        "sentiment": "neutral",
        "interestingness": 0.7085509373685894
      }
    }
  },
  {
    "status": "success",
    "code": 200,
    "result": {
      "text": "I love bowling with friends",
      "peoplepattern": {
        "interests": [
          "leisure_sports"
        ],
        "languages": [
          "en"
        ],
        "sentiment": "positive",
        "interestingness": 0.5522605037296693
      }
    }
  },
  {
    "status": "success",
    "code": 200,
    "result": {
      "text": "But I also love eating at home with the family",
      "peoplepattern": {
        "interests": [
          "family"
        ],
        "languages": [
          "en"
        ],
        "sentiment": "positive",
        "interestingness": 0.5893891902193789
      }
    }
  }
]
```

When passing a batch of posts to the enrich post endpoint,
the client receives a batch of responses. Since each post request
may succeed or fail individually, the batch of responses included
their own meta-data with respect to the response status.

<aside class="notice">
As with the single-post call, batches of Twitter API format "tweets"
are also supported.
</aside>

### Error Sample

To see a comprehensive list of error status returned the the People Pattern Audience Intelligence API please see the [Errors section](#errors).  
Here we have displayed what a same error response would look like from the Enrich API.

> Example invalid format call with output

```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/post" \
  -d '[{}]'

[{"status":"error","code":400,"error":{"input":{},"message":"No valid fields provided for profile content"}}]
```
