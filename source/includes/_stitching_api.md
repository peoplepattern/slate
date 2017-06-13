# Stitching API

The Stitching API exposes a model which attempts to match an individual's name, location, and/or email address to a Twitter account.  People Pattern’s stitching algorithms process, identify, score and match social profiles to individuals, adding dimensions of customer attributes previously unattainable

Stitching supports the following services:

- `twitter`

<aside class="success">
Providing more information to the API will increase the likelihood of better matches and increased match rates. Providing just one of the accepted fields (name, location, email address) will be unlikely to produce satisfactory results.
</aside>

## Stitch (input)

Persons are objects containing any of the following fields. These are
provided to the stitch [Stitching API](#stitching-api) endpoints

field         | type            | description
--------------|-----------------|------------
`name`        | string          | the first and last name of the person
`email`       | string          | the person's email address, typically the same one used for the social account(s)
`location`    | string          | the text representation of the person's location

All fields are optional, but a person object containing *none* of these fields is considered a bad request, and the more fields submitted increase the quality of matches returned.

## Stitch a single record

When stitching a person record the original person record is passed back along with an array of possible matches.

### Resource URI stitch

`/stitch`

### HTTP POST
To stitch a person record to a social profile, make an HTTP POST request to [Stitching endpoint](#resource-uri-stitch).
The appropriate headers and default body schema can be seen in the example request in the sidebar.

#### POST PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|------------
`body`        | Yes      | a [person record](#stitch-input) or an array of person objects

### Stitch a single person record

```shell
curl "https://stitching.peoplepattern.com/stitch?access_token=$MY_TOKEN" \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
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

Each match will contain a score indicating the confidence of that match.  When passing a single [person record](#stitch-input) to the
stitch endpoint, the array of results are passed
back to the client with a score indicating the confidence of each match.

### Stitch a batch of records

```shell
curl 'https://stitching.peoplepattern.com/stitch?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '[{"query":{"name":"Elias Ponvert","location":"Austin, Texas"}},{"query":{"name":"Jason Baldridge","location":"Austin, Texas"}}]'
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

When passing a batch of person records to the stitch endpoint, POST an array of query JSON objects rather than just a single one.

<aside class="warning">
This API does not currently paginate responses, so as a precaution you should avoid sending arrays of more than 10 queries at a time.
</aside>

## Requesting Additional Fields

```shell
curl "https://stitching.peoplepattern.com/stitch?access_token=$MY_TOKEN" \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"query":{"name":"Elias Ponvert","location":"Austin, Texas"},"fields":["name", "twitter", "peoplepattern"]}'
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
