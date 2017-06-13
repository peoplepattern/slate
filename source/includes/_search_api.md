# Search API

The Search API allows you to search the Portrait database (PDB) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  

Search supports the following services:

- `foursquare`
- `googleplus`
- `instagram`
- `tumblr`
- `twitter`
- `youtube`

To restrict results to just one or just several services, add a clause to your queryString like:

  provider.id:'twitter'
  provider.id:'twitter' OR provider.id:'instagram'

This endpoint supports both HTTP POST and HTTP GET calls.

## Profile Search

Search the PDB by defining a search string using specific demographic and psychographic criteria.  This will return 0 or more profiles that match the submitted criteria.  The search syntax is based on <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a>

The `queryString` parameter is the easiest to use, but we also provide a way to search with any valid elasticsearch `_search` request.  Reach out to our support team if your search is more complex than you can express using `queryString`.

The search results will include all enrichments and predictions for each profile returned.  The available enriched set of fields may not be the same across all profiles.

### Resource URI

`/search`

### Json Schema

type                     | schema URL
-------------------------|-----------
Search Request        | [http://apidocs.peoplepattern.com/schemata/SearchRequest.json](http://apidocs.peoplepattern.com/schemata/SearchRequest.json)
Search Response       | [http://apidocs.peoplepattern.com/schemata/SearchResponse.json](http://apidocs.peoplepattern.com/schemata/SearchResponse.json)

### GET Parameters

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`queryString` | Yes      |  <a href="https://lucene.apache.org/core/2_9_4/queryparsersyntax.html">Lucene</a> formatted query
`fields`      | No       | an array of [PDB fields](#pdb-fields) to be returned for each discovered profile.  Not including this parameter will return all fields.
`limit`       | No       | the maximum number of profiles to return in the result set
`random`      | No       | if true, return a random set of 'limit' matching profiles
`sortField`   | No       | a numeric [PDB field](#pdb-fields) to be used to sort
`sortOrder`   | No       | ASC or DESC

### GET Example

```shell
curl "https://api.peoplepattern.com/search?access_token=$MY_TOKEN&queryString=joe&limit=2" \
  -H "Accept: application/json"
```

```json
{
	"totalItems": 55659,
	"items": [
    {
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
  	}
	]
}
```

### POST Example
```shell
curl "https://api.peoplepattern.com/search?access_token=$MY_TOKEN" \
  -X POST \
  -H "Accept: application/json" \
  -d '{"queryString":"john", "limit":"2","random":"true"}'
```

```json
{
	"totalItems": 55659,
	"items": [
    {
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
  	}
  ]
}
```
