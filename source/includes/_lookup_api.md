# Lookup API

The Lookup API provides access to our Portrait database (Pdb) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  
This endpoint supports both HTTP POST and HTTP GET calls.


## Portrait Lookup

Retrieve one or more profiles from the Pdb by submitting their relevenat social profile identifiers.  If found, an enriched profile (referred to as a portrait) will be returned.

Our currently supported services are

- `twitter`
- `instagram`

### Resource URI

`/pdb/lookup`

### HTTP GET

To lookup a profile, make an HTTP GET request to [PDB Lookup endpoint](#resource-uri).  

#### GET PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`ids`         | Yes      | the social ids to lookup, in the format "$service:$service_id" ie. "twitter:12345"
`fields`      | No       | an array of [Pdb fields](#pdb-fields) to be returned for each discovered profile.  Not including this parameter will return all fields.

### Lookup a single profile

```shell
curl 'https://api.peoplepattern.com/pdb/lookup?id=twitter:14132201' \
  -H "Authorization: secretkey" \
  -H "Accept: application/json" 
```

```json
{
  "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
  "twitter": {
    "statuses_count": 1995,
    "followers_count": 2162,
    "friends_count": 1905,
    "lang": "en",
    "listed_count": 132,
    "screen_name": "chonuff",
    "favourites_count": 375
  },
  "enrichments": {
    "psychographics": {
      "interests": {
        "business": 36,
        "small_business": 23,
        "major_sports": 36,
        "leisure_sports": 4,
        "consumer_electronics": 45,
        "charity": 3,
        "beverages": 39,
        "computers": 25,
        "current_events": 4,
        "other_sports": 39,
        "science": 21,
        "tv": 3,
        "finance": 5,
        "design": 5,
        "school_life": 6,
        "shopping": 36,
        "food": 66,
        "marketing": 49,
        "travel": 3,
        "parenting": 4,
        "family": 3,
        "reading": 5,
        "art": 39,
        "politics": 6,
        "beauty": 3,
        "environmentalism": 5,
        "higher_education": 6
      },
      "languages": {
        "en": 193,
        "it": 6,
        "fr": 6,
        "pt": 3
      },
      "mentions": [
        "twitter:1115726696",
        "twitter:14132201",
        "twitter:119837224",
        "twitter:2467338618",
        "twitter:135486789",
        "twitter:60642052",
        "twitter:16031509",
        "twitter:3193477555",
        "twitter:61546029",
        "twitter:78691237",
        "twitter:100054113",
        "twitter:10069172",
        "twitter:1043358110",
        "twitter:11833202",
        "twitter:123060735",
        "twitter:1322691",
        "twitter:1347753500",
        "twitter:14800270",
        "twitter:153229750",
        "twitter:1536791610"
      ],
      "hashtags": [
        "CannesLions",
        "PPinCannes",
        "Branding",
        "CulturatiSummit",
        "analytics",
        "atx",
        "bisongrove2015",
        "datapopupaustin",
        "design",
        "entrepreneur",
        "mrx",
        "socialmedia",
        "sxsw",
        "AI",
        "ATX",
        "AWXII",
        "Advocate",
        "AudienceInsights",
        "BigData",
        "BroLove"
      ]
    },
    "demographics": {
      "race": "east-asian",
      "birthyear": 1972,
      "gender": "male"
    },
    "account_type": "person",
    "version": "0.10",
    "vcard": {
      "name": {
        "fn": "Kenneth Cho"
      }
    },
    "interestingness": 0.977957927320845
  },
  "screenName": "chonuff",
  "objectType": "profile",
  "createdAt": "2016-03-16T18:03:20.429Z",
  "id": "twitter:14132201",
  "displayScreenName": "chonuff",
  "updatedAt": "2016-03-16T18:03:20.429Z",
  "provider": {
    "id": "twitter"
  },
  "published": "2016-03-16T18:03:20.429Z",
  "displayName": "Kenneth Cho",
  "image": {
    "url": "https://pbs.twimg.com/profile_images/531528884588511232/VB-ZMgWI_normal.jpeg"
  },
  "summary": "Co-founder of @PeoplePattern & @Spredfast. Father of 2 bon vivants. Played college ball & the clarinet.",
  "indexedAt": "2015-11-04T05:24:24.739Z",
  "url": "http://t.co/iedzuEKtSM",
  "location": "Austin"
}
```

When looking up a profile the response will include the submitted social platform identifier, if a profile is not found in the Pdb it is left out of the response.

### Lookup a batch of profiles

```shell
curl 'https://api.peoplepattern.com/pdb/lookup?id=twitter:14132201,twitter:119837224&fields=displayName' \
  -H "Authorization: secretkey" \
  -H "Accept: application/json" 
```

```json
{
  "twitter:14132201": {
    "displayName": "Kenneth Cho"
  },
  "twitter:119837224": {
    "displayName": "Jason Baldridge"
  }
}
```

When looking up a batch of profiles the response will include each submitted social platform identifier, if a profile is not found in the Pdb it is left out of the response.

### HTTP POST

To lookup a profile, make an HTTP POST request to [PDB Lookup endpoint](#resource-uri).  

#### POST PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`body`        | Yes      | an array of [Pdb fields](#pdb-fields) to be returned for each discovered profile and a second array of the social ids to lookup, in the format "$service:$service_id" ie. "twitter:12345"


### Lookup a single profile

```shell
curl 'https://api.peoplepattern.com/pdb/lookup \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Accept: application/json" \
  -d '{"ids": ["twitter:14132201"]}'
```

```json
{
  "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
  "twitter": {
    "statuses_count": 1995,
    "followers_count": 2162,
    "friends_count": 1905,
    "lang": "en",
    "listed_count": 132,
    "screen_name": "chonuff",
    "favourites_count": 375
  },
  "enrichments": {
    "psychographics": {
      "interests": {
        "business": 36,
        "small_business": 23,
        "major_sports": 36,
        "leisure_sports": 4,
        "consumer_electronics": 45,
        "charity": 3,
        "beverages": 39,
        "computers": 25,
        "current_events": 4,
        "other_sports": 39,
        "science": 21,
        "tv": 3,
        "finance": 5,
        "design": 5,
        "school_life": 6,
        "shopping": 36,
        "food": 66,
        "marketing": 49,
        "travel": 3,
        "parenting": 4,
        "family": 3,
        "reading": 5,
        "art": 39,
        "politics": 6,
        "beauty": 3,
        "environmentalism": 5,
        "higher_education": 6
      },
      "languages": {
        "en": 193,
        "it": 6,
        "fr": 6,
        "pt": 3
      },
      "mentions": [
        "twitter:1115726696",
        "twitter:14132201",
        "twitter:119837224",
        "twitter:2467338618",
        "twitter:135486789",
        "twitter:60642052",
        "twitter:16031509",
        "twitter:3193477555",
        "twitter:61546029",
        "twitter:78691237",
        "twitter:100054113",
        "twitter:10069172",
        "twitter:1043358110",
        "twitter:11833202",
        "twitter:123060735",
        "twitter:1322691",
        "twitter:1347753500",
        "twitter:14800270",
        "twitter:153229750",
        "twitter:1536791610"
      ],
      "hashtags": [
        "CannesLions",
        "PPinCannes",
        "Branding",
        "CulturatiSummit",
        "analytics",
        "atx",
        "bisongrove2015",
        "datapopupaustin",
        "design",
        "entrepreneur",
        "mrx",
        "socialmedia",
        "sxsw",
        "AI",
        "ATX",
        "AWXII",
        "Advocate",
        "AudienceInsights",
        "BigData",
        "BroLove"
      ]
    },
    "demographics": {
      "race": "east-asian",
      "birthyear": 1972,
      "gender": "male"
    },
    "account_type": "person",
    "version": "0.10",
    "vcard": {
      "name": {
        "fn": "Kenneth Cho"
      }
    },
    "interestingness": 0.977957927320845
  },
  "screenName": "chonuff",
  "objectType": "profile",
  "createdAt": "2016-03-16T18:03:20.429Z",
  "id": "twitter:14132201",
  "displayScreenName": "chonuff",
  "updatedAt": "2016-03-16T18:03:20.429Z",
  "provider": {
    "id": "twitter"
  },
  "published": "2016-03-16T18:03:20.429Z",
  "displayName": "Kenneth Cho",
  "image": {
    "url": "https://pbs.twimg.com/profile_images/531528884588511232/VB-ZMgWI_normal.jpeg"
  },
  "summary": "Co-founder of @PeoplePattern & @Spredfast. Father of 2 bon vivants. Played college ball & the clarinet.",
  "indexedAt": "2015-11-04T05:24:24.739Z",
  "url": "http://t.co/iedzuEKtSM",
  "location": "Austin"
}
```

When looking up a profile the response will include the submitted social platform identifier, if a profile is not found in the Pdb it is left out of the response.

### Lookup a batch of profiles

```shell
curl 'https://api.peoplepattern.com/pdb/lookup?' \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Accept: application/json" \
  -d '{"fields": ["displayName"],"ids": ["twitter:14132201","twitter:119837224"]}'

```

```json
{
  "twitter:14132201": {
    "displayName": "Kenneth Cho"
  },
  "twitter:119837224": {
    "displayName": "Jason Baldridge"
  }
}
```

When looking up a batch of profiles the response will include each submitted social platform identifier, if a profile is not found in the Pdb it is left out of the response.
