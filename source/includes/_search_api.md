# Search API

The Search API allows you to search the Portrait database (Pdb) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  

Search supports the following services:

- `foursquare`
- `googleplus`
- `instagram`
- `tumblr`
- `twitter`
- `youtube`

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
    "$schema": "http://apidocs.peoplepattern.com/pdb-profile.json",
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
    "$schema": "http://apidocs.peoplepattern.com/pdb-profile.json",
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
    "$schema": "http://apidocs.peoplepattern.com/pdb-profile.json",
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
    "$schema": "http://apidocs.peoplepattern.com/pdb-profile.json",
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
{
	"totalItems": 55659,
	"items": [{
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "Jordyn Derham",
		"handle": "heyjordynnn",
		"location": "",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 8279,
			"followers_count": 654,
			"friends_count": 620,
			"listed_count": 1,
			"statuses_count": 11112,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"birthyear": 1984,
				"age": 33
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Jordyn",
					"family_name": "Derham",
					"fn": "Jordyn Derham"
				}
			},
			"interestingness": 0.5293136029467735,
			"version": "0.11.3.1-RC2",
			"influence": 34
		},
		"id": "twitter:449475865",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/640008864969162752/gRLm24sx_normal.jpg"
		},
		"summary": "osu18 joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe",
		"published": "2011-12-29T04:47:04.000Z",
		"service_id": "449475865",
		"lang": "en",
		"posts": {
			"count": 11112
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "Mimi ☺",
		"handle": "karlaperazal",
		"location": "Cheer; my first true love❤",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 3578,
			"followers_count": 1156,
			"friends_count": 1224,
			"listed_count": 0,
			"statuses_count": 22165,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"race": "white",
				"gender": "female"
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Mimi",
					"family_name": "Peraza",
					"fn": "Mimi Peraza"
				}
			},
			"interestingness": 0.7487148062153075,
			"version": "0.11.3.1-RC2",
			"influence": 39
		},
		"id": "twitter:307534922",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/550208318103642113/-5yGhgR3_normal.jpeg"
		},
		"summary": "Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤Joe Luque❤",
		"published": "2011-05-29T20:24:52.000Z",
		"service_id": "307534922",
		"lang": "es",
		"posts": {
			"count": 22165
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "★ joe",
		"handle": "jszulueta",
		"location": "Manila",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 3,
			"followers_count": 48,
			"friends_count": 86,
			"listed_count": 0,
			"statuses_count": 708,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": true,
			"demographics": {
				"birthyear": 1977,
				"race": "south-asian",
				"gender": "male",
				"age": 40
			},
			"psychographics": {
				"languages": {
					"eu": 0.0072992700729927005,
					"tl": 0.051094890510948905,
					"en": 0.9197080291970803,
					"und": 0.0072992700729927005,
					"it": 0.0072992700729927005,
					"es": 0.0072992700729927005
				},
				"interests": {
					"other_sports": 0.0136986301369863,
					"beauty": 0.00684931506849315,
					"environmentalism": 0.0136986301369863,
					"movies": 0.00684931506849315,
					"humor": 0.0273972602739726,
					"music": 0.00684931506849315,
					"health_care": 0.02054794520547945,
					"design": 0.02054794520547945,
					"military": 0.0410958904109589,
					"dating": 0.00684931506849315,
					"parenting": 0.00684931506849315,
					"computers": 0.0136986301369863,
					"shopping": 0.0273972602739726,
					"local_life": 0.07534246575342465,
					"gaming": 0.00684931506849315,
					"beverages": 0.02054794520547945,
					"business": 0.0136986301369863,
					"current_events": 0.00684931506849315,
					"consumer_electronics": 0.03424657534246575,
					"food": 0.0410958904109589,
					"outdoor_recreation": 0.00684931506849315,
					"religion": 0.02054794520547945,
					"crafts": 0.00684931506849315,
					"multimedia": 0.3561643835616438,
					"science": 0.02054794520547945,
					"toys_and_games": 0.00684931506849315,
					"school_life": 0.00684931506849315,
					"travel": 0.1506849315068493,
					"family": 0.0136986301369863
				},
				"sentiment": {
					"negative": 0.031496062992125984,
					"neutral": 0.7637795275590551,
					"positive": 0.2047244094488189
				},
				"top_languages": ["en", "tl", "es"],
				"top_interests": ["multimedia", "travel", "local_life", "food", "military"]
			},
			"place": {
				"city": true,
				"geo_name_id": 1701668,
				"type": "City",
				"name": "Manila, Philippines",
				"location": {
					"city": "Manila",
					"state": "Metro Manila",
					"state_abbreviation": "NCR",
					"time_zone": "Asia/Manila",
					"metro_area": "Quezon City, Philippines",
					"continent": "AS",
					"population": 1600000,
					"place_type": "City",
					"country": "Philippines",
					"country_code": "PH",
					"coordinates": {
						"longitude": 120.9822,
						"latitude": 14.6042
					}
				},
				"global_metro_area": "Manila, Philippines"
			},
			"vcard": {
				"name": {
					"given_name": "Joe",
					"family_name": "Zulueta",
					"fn": "Joe Zulueta"
				}
			},
			"interestingness": 0.6580114462803627,
			"version": "0.11.3.1-RC2",
			"influence": 19
		},
		"id": "twitter:130573602",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/491912407841644544/7dD2PrDr_normal.jpeg"
		},
		"summary": "joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe",
		"published": "2010-04-07T17:56:08.000Z",
		"service_id": "130573602",
		"lang": "en",
		"posts": {
			"top_hashtags": ["3d", "fps", "mobile", "pg3d", "pixelgun", "pixelgun3d", "shooter", "HiddenRisks", "TheSMStoreMakati3DS", "WaltDisney", "gifersation"],
			"os": {
				"android": 0.4444444444444444,
				"ios": 0.5555555555555556
			},
			"devices": {
				"desktop": 0.04,
				"mobile": 0.96
			},
			"top_domains": ["fb.me", "4sq.com", "goo.gl", "instagr.am", "www.viber.com", "bit.ly", "huff.to", "ph.sharings.cc", "play.google.com", "wechat.com"],
			"count": 708,
			"top_mentions": ["twitter:960481315", "twitter:122302784", "twitter:14120151", "twitter:2166412230", "twitter:2576461322", "twitter:15092616", "twitter:3746042353", "twitter:71983360", "twitter:106915372", "twitter:14511951", "twitter:326380075", "twitter:335942140", "twitter:347258974", "twitter:871351657"]
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "super Joe kelly",
		"handle": "SuPeRJoEKeLlY",
		"location": "",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 0,
			"followers_count": 58,
			"friends_count": 136,
			"listed_count": 0,
			"statuses_count": 3,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"birthyear": 1983,
				"race": "white",
				"gender": "male",
				"age": 34
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Super",
					"family_name": "Kelly",
					"fn": "Super Kelly"
				}
			},
			"interestingness": 0.7677059520465661,
			"version": "0.11.3.1-RC2",
			"influence": 20
		},
		"id": "twitter:1330050266",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/3481688817/5617b0cf08dfa4706b7d6dad040e7f69_normal.jpeg"
		},
		"summary": "Joe joe super joe,Joe joe super joe kelly",
		"published": "2013-04-05T20:43:03.000Z",
		"service_id": "1330050266",
		"lang": "en",
		"posts": {
			"count": 3
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "Joe McElderry Page",
		"handle": "JMcElderryFPage",
		"location": "",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 0,
			"followers_count": 69,
			"friends_count": 125,
			"listed_count": 0,
			"statuses_count": 39,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"birthyear": 1963,
				"race": "white",
				"gender": "male",
				"age": 54
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Joe",
					"family_name": "Page",
					"fn": "Joe Page"
				}
			},
			"interestingness": 0.7668147231688995,
			"version": "0.11.3.1-RC2",
			"influence": 21
		},
		"id": "twitter:413240858",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/1640600800/Joe_McElderry_Celebrities_Front_Row_Day_Six_dMI-qs2-TAMl_normal.jpg"
		},
		"summary": "Joe McElderry Joe McElderry Joe McElderry Joe McElderry Joe McElderry Joe McElderry Joe McElderry Joe McElderry x",
		"published": "2011-11-15T17:02:50.000Z",
		"service_id": "413240858",
		"lang": "en",
		"posts": {
			"count": 39
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "Stuff",
		"handle": "joe-photo",
		"provider": {
			"id": "tumblr"
		},
		"twitter": {},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"race": "white",
				"gender": "male"
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Joe",
					"family_name": "Stuff",
					"fn": "Joe Stuff"
				}
			},
			"interestingness": 0.7495088055987297,
			"version": "0.11.3.1-RC2"
		},
		"id": "tumblr:joe-photo",
		"image": {
			"url": "https://api.tumblr.com/v2/blog/joe-photo.tumblr.com/avatar"
		},
		"summary": "",
		"url": "http://joe-photo.tumblr.com/",
		"published": "2015-12-07T19:29:21.785Z",
		"service_id": "joe-photo",
		"posts": {}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "Joseph Gallagher",
		"handle": "gallagherisgood",
		"location": "",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 1491,
			"followers_count": 288,
			"friends_count": 329,
			"listed_count": 0,
			"statuses_count": 2257,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"birthyear": 1984,
				"race": "white",
				"gender": "male",
				"age": 33
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Joseph",
					"family_name": "Gallagher",
					"fn": "Joseph Gallagher"
				}
			},
			"interestingness": 0.9003294839947167,
			"version": "0.11.3.1-RC2",
			"influence": 29
		},
		"id": "twitter:929149687",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/2813686105/8f15f431b88ea758cbdcf00150b8bed2_normal.jpeg"
		},
		"summary": "Joe Gallagher doesn't do what Joe Gallagher does for Joe Gallagher. Joe Gallagher does what Joe Gallagher does because he is Joe Gallagher.",
		"published": "2012-11-06T06:39:18.000Z",
		"service_id": "929149687",
		"lang": "en",
		"posts": {
			"count": 2257
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "joena",
		"handle": "johantilberry",
		"location": "",
		"provider": {
			"id": "twitter"
		},
		"twitter": {
			"favourites_count": 4,
			"followers_count": 4,
			"friends_count": 9,
			"listed_count": 0,
			"statuses_count": 14,
			"verified": false
		},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Joena",
					"family_name": "Berry",
					"fn": "Joena Berry"
				}
			},
			"interestingness": 0.49993866618341076,
			"version": "0.11.3.1-RC2",
			"influence": 11
		},
		"id": "twitter:2874358820",
		"image": {
			"url": "http://pbs.twimg.com/profile_images/525458130075803648/pFIg7gLY_normal.jpeg"
		},
		"summary": "joe joe joe",
		"published": "2014-10-24T01:25:17.000Z",
		"service_id": "2874358820",
		"lang": "en",
		"posts": {
			"count": 14
		}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "joe-joint",
		"handle": "joe-joint",
		"provider": {
			"id": "tumblr"
		},
		"twitter": {},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"birthyear": 1990,
				"race": "white",
				"gender": "male",
				"age": 27
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Joe-joint",
					"family_name": "Joe",
					"fn": "Joe-joint Joe"
				}
			},
			"interestingness": 0.7642813799014391,
			"version": "0.11.3.1-RC2"
		},
		"id": "tumblr:joe-joint",
		"image": {
			"url": "https://api.tumblr.com/v2/blog/joe-joint.tumblr.com/avatar"
		},
		"summary": "Rocko floyd zeplin",
		"url": "http://joe-joint.tumblr.com/",
		"published": "2014-07-08T04:25:50.117Z",
		"service_id": "joe-joint",
		"posts": {}
	}, {
		"$schema": "http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.11.0/pdb-pojo/pdb-profile.json",
		"type": "profile",
		"name": "joe-wagner",
		"handle": "joe-wagner",
		"provider": {
			"id": "tumblr"
		},
		"twitter": {},
		"enrichments": {
			"account_type": "person",
			"spam": false,
			"adult": false,
			"demographics": {
				"birthyear": 1987,
				"race": "white",
				"gender": "male",
				"age": 30
			},
			"psychographics": {},
			"vcard": {
				"name": {
					"given_name": "Joe-wagner",
					"family_name": "Wagner",
					"fn": "Joe-wagner Wagner"
				}
			},
			"interestingness": 0.8920150138040867,
			"version": "0.11.3.1-RC2"
		},
		"id": "tumblr:joe-wagner",
		"image": {
			"url": "https://api.tumblr.com/v2/blog/joe-wagner.tumblr.com/avatar"
		},
		"summary": "Asshole extraordinaire.",
		"url": "http://joe-wagner.tumblr.com/",
		"published": "2014-09-02T00:06:17.338Z",
		"service_id": "joe-wagner",
		"posts": {}
	}]
}
```
