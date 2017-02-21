# Aggregate API

The Aggregate API allows you to retrieve aggregate insights from the Portrait database (Pdb) which contains
hundreds of millions of social profiles with pre-calculated demographic and psychographic attributes appended to each.  
This endpoint supports both HTTP POST and HTTP GET calls.


## Aggregate Profiles

Get aggregate insights for a set of profiles by submitting their social profile identifiers to the Pdb.  
Aggregate data is returned for both demographic and psychographic attributes.

### Resource URI

`/aggregate`

### HTTP GET

To retrieve aggregate insights for a set of profiles, make an HTTP GET request to [PDB Aggregate endpoint](#resource-uri) and submit one or more social profile identifiers. 

#### GET PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`ids`         | Yes      | the social ids whose attributes will be aggregated, in the format "$service:$service_id" ie. "twitter:12345"
`fields`      | No       | an array of [Pdb fields](#pdb-fields) to be aggregated and returned for each discovered profile

### Aggregate profile attributes

```shell
curl 'https://api.peoplepattern.com/aggregate?access_token=$MY_TOKEN&fields=peoplepattern.race,peoplepattern.birthyear,peoplepattern.account_type,posts.devices,posts.interests,posts.os,peoplepattern.gender,place.location.city&ids=twitter:14132201,twitter:119837224,twitter:391705374,twitter:20092104' \
  -H "Accept: application/json" 
```

```json
{
  "posts.os": {
    "de": 0.0013839364198635503,
    "pt": 0.00975274939594874,
    "blackberry": 0.017122722477892326,
    "android": 0.303043739365118,
    "ja": 0.03566702873107553,
    "en": 0.10719063699523029,
    "it": 0.0018890186195434076,
    "fr": 0.00433679898354334,
    "ios": 0.4897093384161427,
    "windows": 0.000029898952595411925,
    "es": 0.029368580303910118,
    "mac": 0.0005055513391365339
  },
  "peoplepattern.account_type": {
    "person": 1
  },
  "peoplepattern.gender": {
    "male": 1
  },
  "posts.interests": {
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
  "posts.devices": {
    "tablet": 0.03444261383528846,
    "automated": 0.0034475751633945852,
    "desktop": 0.040294415836302486,
    "mobile": 0.9218153951650144
  },
  "place.location.city": {
    "Austin": 1
  },
  "peoplepattern.birthyear": {
    "1972": 0.3333333333333333,
    "1975": 0.3333333333333333,
    "1993": 0.3333333333333333
  },
  "peoplepattern.race": {
    "white": 0.6666666666666666,
    "east-asian": 0.3333333333333333
  }
}
```

### HTTP POST

To retrieve aggregate insights for a set of profiles, make an HTTP POST request to [PDB Aggregate endpoint](#resource-uri) and submit one or more social profile identifiers. 

#### POST PARAMETERS

PARAMETER     | REQUIRED | DESCRIPTION
--------------|----------|-------------
`body`        | Yes      | an array of [Pdb fields](#pdb-fields) to be aggregated and returned for each discovered profile and a second array of the social ids whose attributes will be aggregated, in the format "$service:$service_id" ie. "twitter:12345"

```shell
curl 'https://api.peoplepattern.com/aggregate?access_token=$MY_TOKEN&' \
  -X POST \
  -H "Accept: application/json" \
  -d '{{"fields":["peoplepattern.race","peoplepattern.birthyear","peoplepattern.account_type","posts.devices","posts.interests","posts.os","peoplepattern.gender","place.location.city"], "ids":["twitter:14132201","twitter:119837224","twitter:391705374","twitter:20092104"]}'
```

```json
{
  "posts.os": {
    "de": 0.0013839364198635503,
    "pt": 0.00975274939594874,
    "blackberry": 0.017122722477892326,
    "android": 0.303043739365118,
    "ja": 0.03566702873107553,
    "en": 0.10719063699523029,
    "it": 0.0018890186195434076,
    "fr": 0.00433679898354334,
    "ios": 0.4897093384161427,
    "windows": 0.000029898952595411925,
    "es": 0.029368580303910118,
    "mac": 0.0005055513391365339
  },
  "peoplepattern.account_type": {
    "person": 1
  },
  "peoplepattern.gender": {
    "male": 1
  },
  "posts.interests": {
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
  "posts.devices": {
    "tablet": 0.03444261383528846,
    "automated": 0.0034475751633945852,
    "desktop": 0.040294415836302486,
    "mobile": 0.9218153951650144
  },
  "place.location.city": {
    "Austin": 1
  },
  "peoplepattern.birthyear": {
    "1972": 0.3333333333333333,
    "1975": 0.3333333333333333,
    "1993": 0.3333333333333333
  },
  "peoplepattern.race": {
    "white": 0.6666666666666666,
    "east-asian": 0.3333333333333333
  }
}
```
