# Aggregate API

The Aggregate API allows you to retrieve aggregate insights from the Portrait database (PDB) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.

Aggregate supports the following services:

- `foursquare`
- `googleplus`
- `instagram`
- `tumblr`
- `twitter`
- `youtube`

## Aggregate Profiles

Get aggregate insights for a set of profiles by submitting their social profile identifiers to the PDB.  
Aggregate data is returned for both demographic and psychographic attributes.

### Resource URI

`/aggregate`

### Json Schema

type                     | schema URL
-------------------------|-----------
Aggregate Request        | [http://apidocs.peoplepattern.com/schemata/AggregateRequest.json](http://apidocs.peoplepattern.com/schemata/AggregateRequest.json)
Aggregate Response       | [http://apidocs.peoplepattern.com/schemata/AggregateResponse.json](http://apidocs.peoplepattern.com/schemata/AggregateResponse.json)

### Aggregate profile attributes

Aggregate supports all enum, numeric, date-time, array, and map fields defined on a [PDB profile](#pdb-profile).

Note that the fields to aggregate must be requested in flattened format (see below).

Also note that map fields must be requested using syntax like `posts.os.*` and `posts.devices.*`.

### GET Example
```shell
curl -X GET \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/aggregate?access_token=$MY_TOKEN&fields=enrichments.demographics.race,enrichments.demographics.birthyear,enrichments.account_type,posts.devices.*,enrichments.psychographics.top_interests,posts.os.*,enrichments.demographics.gender,place.location.city&ids=twitter:14132201,twitter:119837224,twitter:391705374,twitter:20092104"
```

```json
{
	"enrichments.account_type": {
		"person": 1.0
	},
	"enrichments.psychographics.top_interests": {
		"marketing": 0.06666666666666667,
		"business": 0.13333333333333333,
		"current_events": 0.06666666666666667,
		"major_sports": 0.06666666666666667,
		"small_business": 0.06666666666666667,
		"fitness": 0.06666666666666667,
		"science": 0.13333333333333333,
		"health_care": 0.06666666666666667,
		"higher_education": 0.06666666666666667,
		"reading": 0.06666666666666667,
		"family": 0.06666666666666667,
		"computers": 0.13333333333333333
	},
	"enrichments.demographics.gender": {
		"male": 1.0
	},
	"enrichments.demographics.race": {
		"white": 0.6666666666666666,
		"east-asian": 0.3333333333333333
	},
	"posts.os.*": {
		"blackberry": 0.0,
		"android": 0.0,
		"ios": 1.0,
		"windows": 0.0,
		"mac": 0.0,
		"unknown": 0.0
	},
	"posts.devices.*": {
		"tablet": 0.0,
		"automated": 0.0,
		"desktop": 0.004219409282700422,
		"mobile": 0.9957805907172995,
		"unknown": 0.0
	},
	"enrichments.demographics.birthyear": {
		"1975": 0.5,
		"1972": 0.5
	}
}
```

### POST Example
```shell
curl -X POST "https://api.peoplepattern.com/aggregate?access_token=$MY_TOKEN" \
  -H "Accept: application/json" \
  -d '{"fields":["enrichments.demographics.race","enrichments.demographics.birthyear","enrichments.account_type","posts.devices.*","enrichments.psychographics.top_interests","posts.os.*","enrichments.demographics.gender","place.location.city"], "ids":["twitter:14132201","twitter:119837224","twitter:391705374","twitter:20092104"]}'

```

```json
{
	"enrichments.account_type": {
		"person": 1.0
	},
	"enrichments.psychographics.top_interests": {
		"marketing": 0.06666666666666667,
		"business": 0.13333333333333333,
		"current_events": 0.06666666666666667,
		"major_sports": 0.06666666666666667,
		"small_business": 0.06666666666666667,
		"fitness": 0.06666666666666667,
		"science": 0.13333333333333333,
		"health_care": 0.06666666666666667,
		"higher_education": 0.06666666666666667,
		"reading": 0.06666666666666667,
		"family": 0.06666666666666667,
		"computers": 0.13333333333333333
	},
	"enrichments.demographics.gender": {
		"male": 1.0
	},
	"enrichments.demographics.race": {
		"white": 0.6666666666666666,
		"east-asian": 0.3333333333333333
	},
	"posts.os.*": {
		"blackberry": 0.0,
		"android": 0.0,
		"ios": 1.0,
		"windows": 0.0,
		"mac": 0.0,
		"unknown": 0.0
	},
	"posts.devices.*": {
		"tablet": 0.0,
		"automated": 0.0,
		"desktop": 0.004219409282700422,
		"mobile": 0.9957805907172995,
		"unknown": 0.0
	},
	"enrichments.demographics.birthyear": {
		"1975": 0.5,
		"1972": 0.5
	}
}
```

## Search/Aggregate Profiles

We also offer aggregation based on search criteria. The `queryString` parameter is the easiest to use, but we also provide a way to search with any valid elasticsearch `_search` request.  Reach out to our support team if your search is more complex than you can express using `queryString`.

### Resource URI

`/aggregatesearch`

### Json Schema

type                     | schema URL
-------------------------|-----------
AggregateSearch Request        | [http://apidocs.peoplepattern.com/schemata/AggregateSearchRequest.json](http://apidocs.peoplepattern.com/schemata/AggregateSearchRequest.json)
AggregateSearch Response       | [http://apidocs.peoplepattern.com/schemata/AggregateSearchResponse.json](http://apidocs.peoplepattern.com/schemata/AggregateSearchResponse.json)

### GET Example
```shell
curl -X GET \
  -H "Accept: application/json"
  "https://api.peoplepattern.com/aggregate?access_token=$MY_TOKEN&fields=enrichments.demographics.race,enrichments.demographics.birthyear,enrichments.account_type,posts.devices.*,enrichments.psychographics.top_interests,posts.os.*,enrichments.demographics.gender,place.location.city&queryString=john" \
```

```json
{
	"enrichments.account_type": {
		"entertainment": 1.8391506376973333E-4,
		"person": 0.9947953288076048,
		"organization": 0.005020756128625441
	},
	"enrichments.psychographics.top_interests": {
		"politics": 0.035818697462143584,
		"other_sports": 0.03053666076128402,
		"gaming": 0.02761313182126375,
		"beverages": 0.023741825419391526,
		"current_events": 0.037120068823224925,
		"business": 0.030066417328288242,
		"consumer_electronics": 0.025108812143216464,
		"higher_education": 0.02272478729686577,
		"food": 0.02682574746834059,
		"religion": 0.04243855850338648,
		"multimedia": 0.02148538600059783,
		"humor": 0.0640369487398205,
		"music": 0.03406895445564766,
		"major_sports": 0.06896174624352049,
		"school_life": 0.038760452891814845,
		"animals": 0.020428249600839877,
		"family": 0.056301626531936454,
		"travel": 0.026927815810386183,
		"automotive": 0.024911966054985673,
		"finance": 0.02719027726136057
	},
	"enrichments.demographics.gender": {
		"female": 0.011415977072219231,
		"male": 0.9885840229277808
	},
	"enrichments.demographics.race": {
		"middle-eastern": 2.807261232695993E-4,
		"white": 0.8984420511505714,
		"south-asian": 0.001572390829180588,
		"hispanic": 0.051822366894438865,
		"black": 0.034495236580723364,
		"east-asian": 0.013387228421816152
	},
	"posts.os.*": {
		"blackberry": 0.02681955952155928,
		"android": 0.3538655259396014,
		"ios": 0.6097575035076012,
		"windows": 9.160855311759634E-4,
		"mac": 0.003519898918088746,
		"unknown": 0.005121426581973373
	},
	"posts.devices.*": {
		"tablet": 0.054544731549693456,
		"automated": 0.003470887228310001,
		"desktop": 0.0428197705361852,
		"mobile": 0.8949874598895574,
		"unknown": 0.004177150796253883
	},
	"enrichments.demographics.birthyear": {
		"1990": 0.021262022202317505,
		"1987": 0.049928869902849664,
		"1986": 0.06093680972395037,
		"1997": 0.02167137489816845,
		"1985": 0.06690282129120378,
		"1996": 0.03187276831853314,
		"1984": 0.0660516919235929,
		"1995": 0.033445331150118954,
		"1983": 0.05902784814230883,
		"1994": 0.028342607941442298,
		"1982": 0.04858732789961537,
		"1993": 0.023130453814072815,
		"1981": 0.037976581783399736,
		"1992": 0.01916662275919929,
		"1980": 0.028820861586099842,
		"1991": 0.018692422111530372,
		"1979": 0.021675427895157074,
		"1968": 0.018218221463861452,
		"1989": 0.027896778272693743,
		"1988": 0.03941944871134961
	}
}
```

### POST Example
```shell
curl -X POST "https://api.peoplepattern.com/aggregate?access_token=$MY_TOKEN" \
  -H "Accept: application/json" \
  -d '{"queryString":"jill","fields":["enrichments.demographics.race","enrichments.demographics.birthyear","enrichments.account_type","posts.devices.*","enrichments.psychographics.top_interests","posts.os.*","enrichments.demographics.gender","place.location.city"]}'
```

```json
{
	"enrichments.account_type": {
		"entertainment": 1.7386356451918822E-4,
		"person": 0.9961275842447999,
		"organization": 0.003698552190680913
	},
	"enrichments.psychographics.top_interests": {
		"politics": 0.023585975416156393,
		"beverages": 0.026942441148455572,
		"business": 0.027169229373610923,
		"current_events": 0.021182020229509685,
		"beauty": 0.018914137977956186,
		"higher_education": 0.025853857667709892,
		"reading": 0.020547013199074704,
		"food": 0.041683675783553316,
		"religion": 0.042908332199392205,
		"multimedia": 0.022542749580441782,
		"humor": 0.0752483331065451,
		"music": 0.02848460107951195,
		"major_sports": 0.03356465732299179,
		"charity": 0.02558171179752347,
		"health_care": 0.024402413026715652,
		"school_life": 0.06327391481834263,
		"animals": 0.0386900712115027,
		"family": 0.09184923118791673,
		"travel": 0.02957318456025763,
		"parenting": 0.024629201251871003
	},
	"enrichments.demographics.gender": {
		"female": 0.9968667493717593,
		"male": 0.003133250628240608
	},
	"enrichments.demographics.race": {
		"middle-eastern": 3.677214142565592E-5,
		"white": 0.9725128242843222,
		"south-asian": 3.1256320211807534E-4,
		"hispanic": 0.01000202246777841,
		"black": 0.009781389619224475,
		"east-asian": 0.007354428285131185
	},
	"posts.os.*": {
		"blackberry": 0.015055618724203267,
		"android": 0.21980291455853063,
		"ios": 0.7600062143666229,
		"windows": 4.383875793916797E-5,
		"mac": 3.5016552631090994E-4,
		"unknown": 0.004741248066393187
	},
	"posts.devices.*": {
		"tablet": 0.06077353367721411,
		"automated": 0.004644188990242093,
		"desktop": 0.03712638231824077,
		"mobile": 0.8936350940424981,
		"unknown": 0.0038208009718047322
	},
	"enrichments.demographics.birthyear": {
		"1987": 0.028461114175399888,
		"1976": 0.014120242691671264,
		"1986": 0.04569773855488141,
		"1985": 0.08066740209597352,
		"1984": 0.11265857694429122,
		"1983": 0.115857694429123,
		"1972": 0.015747380033094317,
		"1982": 0.10157198014340872,
		"1971": 0.0163265306122449,
		"1981": 0.0753723110865968,
		"1970": 0.017539988968560398,
		"1980": 0.050082735797021515,
		"1969": 0.019332597904026475,
		"1979": 0.03143960286817429,
		"1968": 0.017402095973524545,
		"1978": 0.023965802537231108,
		"1967": 0.01643684500827358,
		"1977": 0.0197738554881412,
		"1988": 0.01693325979040265,
		"1966": 0.0151130722559294
	}
}
```
