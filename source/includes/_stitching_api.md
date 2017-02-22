# Stitching API

The Stitching API exposes a model which attempts to match an individual's name, location, and/or email address to a Twitter account.

You should provide as much information to the API as you can. Providing just one of the accepted fields (name, location, email address) will be unlikely to produce satisfactory results -- endeavor to provide at least two of the three fields, and ideally provide all three.

## Querying the API

```shell
curl -H 'Content-type: application/json' -s -u $APIAUTH \
https://stitching.peoplepattern.com/stitch \
-d '{"query":{"name":"Elias Ponvert","location":"Austin, Texas"}}'
```
```json
{
  "hits": {
    "hits": [
      {
        "handle": "eponvert",
        "provider": {
          "id": "twitter"
        },
        "service_id": "61546029",
        "id": "twitter:61546029",
        "_score": 10
      }
    ],
    "total": 1
  }
}
```

The relevant endpoint is located at `https://stitching.peoplepattern.com/stitch`. To query the API, send an HTTP POST request to that endpoint. The appropriate headers and default body schema can be seen in the example request in the sidebar.

### Batch Requests
```shell
> This is what the POST body should look like. Information on
> how to make a basic call to the API can be found above.
[
  {
    "query": {
      "name": "Elias Ponvert",
      "location": "Austin Texas"
    }
  },
  {
    "query": {
      "name": "Jason Balridge",
      "location": "Austin Texas"
    }
  }
]
```
```json
[
  {
    "hits": {
      "hits": [
        {
          "handle": "eponvert",
          "provider": {
            "id": "twitter"
          },
          "service_id": "61546029",
          "id": "twitter:61546029",
          "_score": 10
        }
      ],
      "total": 1
    }
  },
  {
    "hits": {
      "hits": [
        {
          "handle": "jasonbaldridge",
          "provider": {
            "id": "twitter"
          },
          "service_id": "119837224",
          "id": "twitter:119837224",
          "_score": 10
        }
      ],
      "total": 1
    }
  }
]
```

You can also send batch requests to the API. To do so, POST an array of query JSON objects rather than just a single one. An example POST body / response pair can be seen in the sidebar.

<aside class="warning">
This API does not currently paginate responses, so as a precaution you should avoid sending arrays of more than 10 queries at a time.
</aside>

### Requesting Additional Fields

```shell
{
  "query": {
    "name": "Elias Ponvert",
    "location": "Austin Texas"
  },
  "fields": ["name", "twitter", "peoplepattern"]
}
```
```json
{
  "hits": {
    "hits": [
      {
        "peoplepattern": {
          "account_type": "person",
          "birthyear": 1979,
          "gender": "male",
          "race": "white",
          "interestingness": 0.9938160676130328,
          "ageQuantiles": [
            29,
            29.25,
            29.5,
            29.75,
            30,
            30.25,
            30.5,
            31.303387682248616,
            32.860457271189546
          ],
          "numAgeQuantiles": 9,
          "adult": false,
          "spam": false,
          "version": "0.10",
          "age": 37
        },
        "name": "elias ponvert",
        "twitter": {
          "friends_count": 1233,
          "listed_count": "27",
          "screen_name": "eponvert",
          "statuses_count": 857,
          "favourites_count": 87,
          "followers_count": 417,
          "verified": false
        },
        "_score": 10
      }
    ],
    "total": 1
  }
}
```

You can request that the response you receive be annotated with additional fields for each match found. Those additional fields are:

`"name"`: Requesting this field simply appends the matched user's "name" field from Twitter to the response.

`"twitter"`: Requesting this field appends other basic information about the Twitter account such as number of followers, number of tweets, whether the user is "Verified", etc.

`"peoplepattern"`: Requesting this field appends some basic predictions from our other models to the response. This includes predictions of account type, some demographic information, and an "interestingness" score.

An example POST body / response pair can be seen in the sidebar to the right.
