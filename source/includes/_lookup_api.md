# Lookup API

The Lookup API provides access to the Portrait database (Pdb) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  
This endpoint supports both HTTP POST and HTTP GET calls.


## Profile Lookup

Retrieve one or more profiles from the Pdb by submitting their relevant social profile identifiers.  If found, an enriched profile (referred to as a portrait) will be returned.

Our currently supported services are

- `twitter`
- `instagram`

### Resource URI

`/lookup`

### HTTP GET

To lookup a profile, make an HTTP GET request to [PDB Lookup endpoint](#resource-uri).  

#### GET PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`ids`         | Yes      | the social ids to lookup, in the format "$service:$service_id" ie. "twitter:12345"
`fields`      | No       | an array of [Pdb fields](#pdb-fields) to be returned for each discovered profile.  Not including this parameter will return all fields.

### Lookup a single profile

```shell
curl 'https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN&id=twitter:14132201' \
  -H "Accept: application/json"
```

```json
{
  "$schema": "http://apidocs.peoplepattern.com/pdb-profile.json",
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
    "account_type": "person",
    "version": "0.10",
    "vcard": {
      "name": {
        "fn": "Kenneth Cho"
      }
    },
    "interestingness": 0.977957927320845,
    "demographics": {
      "race": "east-asian",
      "birthyear": 1972,
      "gender": "male"
    },
    "psychographics": {
      "interests": {
        "home_and_garden": 0.006479821830880409,
        "tv": 0.017470695748115647,
        "beauty": 0.017265940367377122,
        "movies": 0.02177315693013945,
        "leisure_sports": 0.009359929069074303,
        "humor": 0.05750853899653545,
        "music": 0.04453033527860939,
        "charity": 0.015467887059796497,
        "fitness": 0.016594441298240083,
        "health_care": 0.022492142517216828,
        "military": 0.012983604616798233,
        "animals": 0.02020837619203906,
        "dance": 0.012504671719420499,
        "parenting": 0.023518926659109336,
        "shopping": 0.01430083006408126,
        "beverages": 0.019798850600224946,
        "higher_education": 0.01997958349109464,
        "crafts": 0.005390732786789505,
        "nutrition": 0.008311260662030395,
        "extreme_sports": 0.004636000996369334,
        "science": 0.011792384132337875,
        "toys_and_games": 0.004752356058075963,
        "automotive": 0.016710738588036646,
        "other_sports": 0.017730743716451315,
        "politics": 0.03613494964024038,
        "small_business": 0.010448134933390618,
        "environmentalism": 0.010380695857038939,
        "design": 0.00640181713543588,
        "dating": 0.022347794419577065,
        "cooking": 0.01538251367896448,
        "computers": 0.012205600264598536,
        "local_life": 0.014369243073016447,
        "art": 0.012545077526130427,
        "gaming": 0.018551145567494216,
        "business": 0.02390683426779431,
        "current_events": 0.024671038437982344,
        "consumer_electronics": 0.018596074848357905,
        "reading": 0.018290843933990206,
        "food": 0.029962990997882917,
        "outdoor_recreation": 0.0062732319153118625,
        "religion": 0.04066377046253635,
        "marketing": 0.010551156193984095,
        "multimedia": 0.032531002646433584,
        "major_sports": 0.05873100633715111,
        "school_life": 0.0417529998414586,
        "family": 0.04444678359440516,
        "travel": 0.025538779610336484,
        "finance": 0.02021575505944901,
        "pop_culture": 0.00730116640439448,
        "fashion": 0.016237643973800408
      },
      "languages": {
        "en": 0.95,
        "it": 0.01,
        "fr": 0.01,
        "pt": 0.02
      }
    },
    "posts": {
      "top_mentions": [
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
      "top_hashtags": [
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
    }
  },
  "handle": "chonuff",
  "type": "profile",
  "createdAt": "2016-03-16T18:03:20.429Z",
  "id": "twitter:14132201",
  "displayScreenName": "chonuff",
  "updatedAt": "2016-03-16T18:03:20.429Z",
  "provider": {
    "id": "twitter"
  },
  "published": "2016-03-16T18:03:20.429Z",
  "name": "Kenneth Cho",
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
curl 'https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN&id=twitter:14132201,twitter:119837224&fields=displayName' \
  -H "Accept: application/json"
```

```json
{
  "twitter:14132201": {
    "name": "Kenneth Cho"
  },
  "twitter:119837224": {
    "name": "Jason Baldridge"
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
curl 'https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN \
  -X POST \
  -H "Accept: application/json" \
  -d '{"ids": ["twitter:14132201"]}'
```

```json
{
  "$schema": "http://apidocs.peoplepattern.com/pdb-profile.json",
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
    "account_type": "person",
    "version": "0.10",
    "vcard": {
      "name": {
        "fn": "Kenneth Cho"
      }
    },
    "interestingness": 0.977957927320845,
    "demographics": {
      "race": "east-asian",
      "birthyear": 1972,
      "gender": "male"
    },
    "psychographics": {
      "interests": {
        "home_and_garden": 0.006479821830880409,
        "tv": 0.017470695748115647,
        "beauty": 0.017265940367377122,
        "movies": 0.02177315693013945,
        "leisure_sports": 0.009359929069074303,
        "humor": 0.05750853899653545,
        "music": 0.04453033527860939,
        "charity": 0.015467887059796497,
        "fitness": 0.016594441298240083,
        "health_care": 0.022492142517216828,
        "military": 0.012983604616798233,
        "animals": 0.02020837619203906,
        "dance": 0.012504671719420499,
        "parenting": 0.023518926659109336,
        "shopping": 0.01430083006408126,
        "beverages": 0.019798850600224946,
        "higher_education": 0.01997958349109464,
        "crafts": 0.005390732786789505,
        "nutrition": 0.008311260662030395,
        "extreme_sports": 0.004636000996369334,
        "science": 0.011792384132337875,
        "toys_and_games": 0.004752356058075963,
        "automotive": 0.016710738588036646,
        "other_sports": 0.017730743716451315,
        "politics": 0.03613494964024038,
        "small_business": 0.010448134933390618,
        "environmentalism": 0.010380695857038939,
        "design": 0.00640181713543588,
        "dating": 0.022347794419577065,
        "cooking": 0.01538251367896448,
        "computers": 0.012205600264598536,
        "local_life": 0.014369243073016447,
        "art": 0.012545077526130427,
        "gaming": 0.018551145567494216,
        "business": 0.02390683426779431,
        "current_events": 0.024671038437982344,
        "consumer_electronics": 0.018596074848357905,
        "reading": 0.018290843933990206,
        "food": 0.029962990997882917,
        "outdoor_recreation": 0.0062732319153118625,
        "religion": 0.04066377046253635,
        "marketing": 0.010551156193984095,
        "multimedia": 0.032531002646433584,
        "major_sports": 0.05873100633715111,
        "school_life": 0.0417529998414586,
        "family": 0.04444678359440516,
        "travel": 0.025538779610336484,
        "finance": 0.02021575505944901,
        "pop_culture": 0.00730116640439448,
        "fashion": 0.016237643973800408
      },
      "languages": {
        "en": 0.95,
        "it": 0.01,
        "fr": 0.01,
        "pt": 0.02
      }
    },
    "posts": {
      "top_mentions": [
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
      "top_hashtags": [
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
    }
  },
  "handle": "chonuff",
  "type": "profile",
  "createdAt": "2016-03-16T18:03:20.429Z",
  "id": "twitter:14132201",
  "displayScreenName": "chonuff",
  "updatedAt": "2016-03-16T18:03:20.429Z",
  "provider": {
    "id": "twitter"
  },
  "published": "2016-03-16T18:03:20.429Z",
  "name": "Kenneth Cho",
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
curl 'https://api.peoplepattern.com/lookup?access_token=$MY_TOKEN' \
  -X POST \
  -H "Accept: application/json" \
  -d '{"fields": ["displayName"],"ids": ["twitter:14132201","twitter:119837224"]}'

```

```json
{
  "twitter:14132201": {
    "name": "Kenneth Cho"
  },
  "twitter:119837224": {
    "name": "Jason Baldridge"
  }
}
```

When looking up a batch of profiles the response will include each submitted social platform identifier, if a profile is not found in the Pdb it is left out of the response.
