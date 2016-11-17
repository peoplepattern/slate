# Search API

The Search API allows you to search the Portrait database (Pdb) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  
This endpoint supports both HTTP POST and HTTP GET calls.


## Profile Search

Search the Pdb by defining a search string using specific demographic and psychographic criteria.  This will return 0 or more profiles tha match the submitted criteria.  The search syntax is based on <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a> 

### Resource URI

`/search`

### HTTP GET

To search for a profile, make an HTTP GET request to [PDB Search endpoint](#resource-uri) and submit a <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a> formatted query using the [Pdb fields](#pdb-fields).  

#### GET PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`queryString` | Yes      |  <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a> formatted query
`fields`      | No       | an array of [Pdb fields](#pdb-fields) to be returned for each discovered profile.  Not including this parameter will return all fields.
`limit`       | No       | the maximum number of profiles to return in the result set

### Search for profiles

```shell
curl 'https://api.peoplepattern.com/search?access_token=$MY_TOKEN&queryString=joe&limit=5' \
  -H "Accept: application/json" 
```

```json
[
  {
    "enrichments": {
      "demographics": {
        "gender": "female",
        "race": "white",
        "birthyear": 1997
      },
      "vcard": {
        "name": {
          "fn": "Jordyn Derham"
        }
      },
      "account_type": "person",
      "version": "0.10",
      "interestingness": 0.8605606982400245
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 11112,
      "followers_count": 654,
      "friends_count": 620,
      "lang": "en",
      "screen_name": "heyjordynnn",
      "favourites_count": 8279,
      "listed_count": 1
    },
    "displayName": "Jordyn Derham",
    "screenName": "heyjordynnn",
    "image": {
      "url": "http://pbs.twimg.com/profile_images/640008864969162752/gRLm24sx_normal.jpg"
    },
    "objectType": "profile",
    "id": "twitter:449475865",
    "displayScreenName": "heyjordynnn",
    "summary": "osu18 joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe",
    "indexedAt": "2015-11-04T04:32:02.907Z",
    "provider": {
      "id": "twitter"
    },
    "published": "2011-12-29T04:47:04.000Z",
    "location": ""
  },
  {
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 708,
      "followers_count": 48,
      "friends_count": 86,
      "lang": "en",
      "listed_count": 0,
      "screen_name": "jszulueta",
      "favourites_count": 3
    },
    "enrichments": {
      "psychographics": {
        "languages": {
          "android": 5,
          "ios": 6
        },
        "interests": {
          "business": 2,
          "health_care": 3,
          "military": 6,
          "consumer_electronics": 5,
          "beverages": 3,
          "computers": 2,
          "other_sports": 2,
          "science": 3,
          "crafts": 1,
          "design": 3,
          "religion": 3,
          "shopping": 4,
          "food": 6,
          "local_life": 11,
          "travel": 22,
          "multimedia": 52,
          "family": 2,
          "beauty": 1,
          "environmentalism": 2,
          "humor": 4
        },
        "sentiment": {
          "neutral": 1,
          "positive": 126
        },
        "mentions": [
          "twitter:122302784",
          "twitter:14120151",
          "twitter:2166412230",
          "twitter:960481315",
          "twitter:71983360",
          "twitter:106915372",
          "twitter:14511951",
          "twitter:15092616",
          "twitter:2576461322",
          "twitter:326380075",
          "twitter:347258974",
          "twitter:3746042353",
          "twitter:871351657"
        ],
        "hashtags": [
          "3d",
          "fps",
          "mobile",
          "pg3d",
          "pixelgun",
          "pixelgun3d",
          "shooter",
          "HiddenRisks",
          "TheSMStoreMakati3DS",
          "WaltDisney",
          "gifersation"
        ]
      },
      "demographics": {
        "race": "white",
        "birthyear": 1999,
        "gender": "female"
      },
      "account_type": "person",
      "version": "0.10",
      "vcard": {
        "name": {
          "fn": "Joe Zulueta"
        }
      },
      "interestingness": 0.8452886615186165
    },
    "screenName": "jszulueta",
    "objectType": "profile",
    "id": "twitter:130573602",
    "displayScreenName": "jszulueta",
    "provider": {
      "id": "twitter"
    },
    "published": "2010-04-07T17:56:08.000Z",
    "displayName": "★ joe",
    "image": {
      "url": "http://pbs.twimg.com/profile_images/491912407841644544/7dD2PrDr_normal.jpeg"
    },
    "summary": "joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe",
    "indexedAt": "2015-11-03T23:31:29.870Z",
    "location": "Manila"
  },
  {
    "summary": "I is a joe joe. wuff wuff",
    "enrichments": {
      "demographics": {
        "gender": "male",
        "race": "white",
        "birthyear": 1995
      },
      "account_type": "person",
      "version": "0.10",
      "vcard": {
        "name": {
          "fn": "Joe Joe"
        }
      },
      "interestingness": 0.978578480952993
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.8-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 12,
      "screen_name": "hugh_jass0426",
      "favourites_count": 5,
      "followers_count": 109,
      "listed_count": 0,
      "friends_count": 360,
      "lang": "en"
    },
    "displayName": "Joe Joe",
    "provider": {
      "id": "twitter"
    },
    "image": {
      "url": "http://abs.twimg.com/sticky/default_profile_images/default_profile_5_normal.png"
    },
    "published": "2015-12-20T18:33:19.000Z",
    "objectType": "profile",
    "location": "",
    "id": "twitter:4548839657"
  },
  {
    "summary": "",
    "enrichments": {
      "demographics": {
        "gender": "male",
        "race": "white",
        "birthyear": 1982
      },
      "account_type": "person",
      "version": "0.10",
      "vcard": {
        "name": {
          "fn": "Joe-joe Joe"
        }
      },
      "interestingness": 0.8500681794764976
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.8-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 981,
      "screen_name": "Most_Hated_Joe",
      "favourites_count": 2,
      "followers_count": 82,
      "listed_count": 3,
      "friends_count": 112,
      "lang": "en"
    },
    "displayName": "joe-JOE",
    "provider": {
      "id": "twitter"
    },
    "image": {
      "url": "http://pbs.twimg.com/profile_images/1314498826/ATBJjsRa_normal.jpg"
    },
    "published": "2009-10-24T21:57:52.000Z",
    "objectType": "profile",
    "location": "ALL OVA KEEP UP ",
    "id": "twitter:84947631"
  },
  {
    "enrichments": {
      "demographics": {
        "gender": "male",
        "race": "white",
        "birthyear": 1996
      },
      "vcard": {
        "name": {
          "fn": "Joe-joe Joe"
        }
      },
      "account_type": "person",
      "version": "0.10",
      "interestingness": 0.8505434921767472
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 4,
      "followers_count": 0,
      "friends_count": 1,
      "lang": "en",
      "screen_name": "JOEJOE4924",
      "favourites_count": 0,
      "listed_count": 0
    },
    "displayName": "JOE-JOE",
    "screenName": "JOEJOE4924",
    "image": {
      "url": "http://abs.twimg.com/sticky/default_profile_images/default_profile_1_normal.png"
    },
    "objectType": "profile",
    "id": "twitter:493616250",
    "displayScreenName": "JOEJOE4924",
    "indexedAt": "2015-11-04T04:50:14.461Z",
    "provider": {
      "id": "twitter"
    },
    "published": "2012-02-16T00:25:39.000Z",
    "location": ""
  }
]
```

The search results will include all enrichments and predictions for each profile returned.  Due to availability of data to base predicitions, the enriched set of fields may not be the same across all Pdb profiles.

### HTTP POST

To search for a profile, make an HTTP POST request to [PDB Search endpoint](#resource-uri) and submit a <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a> formatted query using the [Pdb fields](#pdb-fields).  

#### POST PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`body`        | Yes      | {fields:	[an array of [Pdb fields](#pdb-fields) to be returned for each profile that matches the search], limit: the maximum number of profiles to return in the result set as an integer, queryString: a <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a> formatted query as a String }

```shell
curl 'https://api.peoplepattern.com/search?access_token=$MY_TOKEN&' \
  -X POST \
  -H "Authorization: secretkey" \
  -H "Accept: application/json" \
  -d '{"queryString":"john", "limit":"5"}'
```

```json
[
  {
    "enrichments": {
      "demographics": {
        "gender": "female",
        "race": "white",
        "birthyear": 1997
      },
      "vcard": {
        "name": {
          "fn": "Jordyn Derham"
        }
      },
      "account_type": "person",
      "version": "0.10",
      "interestingness": 0.8605606982400245
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 11112,
      "followers_count": 654,
      "friends_count": 620,
      "lang": "en",
      "screen_name": "heyjordynnn",
      "favourites_count": 8279,
      "listed_count": 1
    },
    "displayName": "Jordyn Derham",
    "screenName": "heyjordynnn",
    "image": {
      "url": "http://pbs.twimg.com/profile_images/640008864969162752/gRLm24sx_normal.jpg"
    },
    "objectType": "profile",
    "id": "twitter:449475865",
    "displayScreenName": "heyjordynnn",
    "summary": "osu18 joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe",
    "indexedAt": "2015-11-04T04:32:02.907Z",
    "provider": {
      "id": "twitter"
    },
    "published": "2011-12-29T04:47:04.000Z",
    "location": ""
  },
  {
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 708,
      "followers_count": 48,
      "friends_count": 86,
      "lang": "en",
      "listed_count": 0,
      "screen_name": "jszulueta",
      "favourites_count": 3
    },
    "enrichments": {
      "psychographics": {
        "languages": {
          "android": 5,
          "ios": 6
        },
        "interests": {
          "business": 2,
          "health_care": 3,
          "military": 6,
          "consumer_electronics": 5,
          "beverages": 3,
          "computers": 2,
          "other_sports": 2,
          "science": 3,
          "crafts": 1,
          "design": 3,
          "religion": 3,
          "shopping": 4,
          "food": 6,
          "local_life": 11,
          "travel": 22,
          "multimedia": 52,
          "family": 2,
          "beauty": 1,
          "environmentalism": 2,
          "humor": 4
        },
        "sentiment": {
          "neutral": 1,
          "positive": 126
        },
        "mentions": [
          "twitter:122302784",
          "twitter:14120151",
          "twitter:2166412230",
          "twitter:960481315",
          "twitter:71983360",
          "twitter:106915372",
          "twitter:14511951",
          "twitter:15092616",
          "twitter:2576461322",
          "twitter:326380075",
          "twitter:347258974",
          "twitter:3746042353",
          "twitter:871351657"
        ],
        "hashtags": [
          "3d",
          "fps",
          "mobile",
          "pg3d",
          "pixelgun",
          "pixelgun3d",
          "shooter",
          "HiddenRisks",
          "TheSMStoreMakati3DS",
          "WaltDisney",
          "gifersation"
        ]
      },
      "demographics": {
        "race": "white",
        "birthyear": 1999,
        "gender": "female"
      },
      "account_type": "person",
      "version": "0.10",
      "vcard": {
        "name": {
          "fn": "Joe Zulueta"
        }
      },
      "interestingness": 0.8452886615186165
    },
    "screenName": "jszulueta",
    "objectType": "profile",
    "id": "twitter:130573602",
    "displayScreenName": "jszulueta",
    "provider": {
      "id": "twitter"
    },
    "published": "2010-04-07T17:56:08.000Z",
    "displayName": "★ joe",
    "image": {
      "url": "http://pbs.twimg.com/profile_images/491912407841644544/7dD2PrDr_normal.jpeg"
    },
    "summary": "joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe",
    "indexedAt": "2015-11-03T23:31:29.870Z",
    "location": "Manila"
  },
  {
    "summary": "I is a joe joe. wuff wuff",
    "enrichments": {
      "demographics": {
        "gender": "male",
        "race": "white",
        "birthyear": 1995
      },
      "account_type": "person",
      "version": "0.10",
      "vcard": {
        "name": {
          "fn": "Joe Joe"
        }
      },
      "interestingness": 0.978578480952993
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.8-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 12,
      "screen_name": "hugh_jass0426",
      "favourites_count": 5,
      "followers_count": 109,
      "listed_count": 0,
      "friends_count": 360,
      "lang": "en"
    },
    "displayName": "Joe Joe",
    "provider": {
      "id": "twitter"
    },
    "image": {
      "url": "http://abs.twimg.com/sticky/default_profile_images/default_profile_5_normal.png"
    },
    "published": "2015-12-20T18:33:19.000Z",
    "objectType": "profile",
    "location": "",
    "id": "twitter:4548839657"
  },
  {
    "summary": "",
    "enrichments": {
      "demographics": {
        "gender": "male",
        "race": "white",
        "birthyear": 1982
      },
      "account_type": "person",
      "version": "0.10",
      "vcard": {
        "name": {
          "fn": "Joe-joe Joe"
        }
      },
      "interestingness": 0.8500681794764976
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.8-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 981,
      "screen_name": "Most_Hated_Joe",
      "favourites_count": 2,
      "followers_count": 82,
      "listed_count": 3,
      "friends_count": 112,
      "lang": "en"
    },
    "displayName": "joe-JOE",
    "provider": {
      "id": "twitter"
    },
    "image": {
      "url": "http://pbs.twimg.com/profile_images/1314498826/ATBJjsRa_normal.jpg"
    },
    "published": "2009-10-24T21:57:52.000Z",
    "objectType": "profile",
    "location": "ALL OVA KEEP UP ",
    "id": "twitter:84947631"
  },
  {
    "enrichments": {
      "demographics": {
        "gender": "male",
        "race": "white",
        "birthyear": 1996
      },
      "vcard": {
        "name": {
          "fn": "Joe-joe Joe"
        }
      },
      "account_type": "person",
      "version": "0.10",
      "interestingness": 0.8505434921767472
    },
    "$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json",
    "twitter": {
      "statuses_count": 4,
      "followers_count": 0,
      "friends_count": 1,
      "lang": "en",
      "screen_name": "JOEJOE4924",
      "favourites_count": 0,
      "listed_count": 0
    },
    "displayName": "JOE-JOE",
    "screenName": "JOEJOE4924",
    "image": {
      "url": "http://abs.twimg.com/sticky/default_profile_images/default_profile_1_normal.png"
    },
    "objectType": "profile",
    "id": "twitter:493616250",
    "displayScreenName": "JOEJOE4924",
    "indexedAt": "2015-11-04T04:50:14.461Z",
    "provider": {
      "id": "twitter"
    },
    "published": "2012-02-16T00:25:39.000Z",
    "location": ""
  }
]
```
