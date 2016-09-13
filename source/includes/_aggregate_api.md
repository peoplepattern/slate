# Aggregate API

## Retrieve aggregate insights

### GET pattern

```shell
curl '/pdb/aggregate?type=profile&fields=posts.interests&ids=twitter:201892491'
  -H "Authorization: secretkey" \
  -H'Accept: application/json' 
```

```http
GET /pdb/aggregate?type=profile&fields=posts.interests&ids=twitter:201892491 HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey
```

> Response will look like

```shell
 {"posts.interests":{"home_and_garden":0.00632634510034411,"tv":0.017641091417461792,"beauty":0.01739964801038861,"movies":0.021844295292726947,"leisure_sports":0.009329955966575574,"humor":0.058345876185155875,"music":0.04485514027861094,"charity":0.015389966992934849,"fitness":0.0165814233367729,"health_care":0.021527699213594077,"military":0.013034320299285453,"animals":0.020148544771305524,"dance":0.012551060067223207,"parenting":0.023642682461784918,"shopping":0.01413827847825423,"beverages":0.01989591944350184,"higher_education":0.01992083188540363,"crafts":0.005263564354310484,"nutrition":0.008217999185114544,"extreme_sports":0.0046040907095506066,"science":0.011737067154455726,"toys_and_games":0.004699628710404084,"automotive":0.016683389361043143,"other_sports":0.01786744915770121,"politics":0.03622886489314473,"small_business":0.010401117767321753,"environmentalism":0.010210921567875668,"design":0.0062678792518393875,"dating":0.022562492611140666,"cooking":0.01541533277159928,"computers":0.012154950526783446,"local_life":0.01371711611672098,"art":0.012431124811468516,"gaming":0.018048887641435224,"business":0.02347847262822203,"current_events":0.02491274929978587,"consumer_electronics":0.018235434213545867,"reading":0.0182121319626697,"food":0.030091208884950964,"outdoor_recreation":0.006174227335769481,"religion":0.040720771316832355,"marketing":0.010582783498559166,"multimedia":0.032546506041154,"major_sports":0.059709128166831875,"school_life":0.04198742318776386,"family":0.04478017593705101,"travel":0.025614312842226965,"finance":0.020140523235578984,"pop_culture":0.007421613436708357,"fashion":0.0163075822191156}}
 ```

 ```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1088

{"posts.interests":{"home_and_garden":0.00632634510034411,"tv":0.017641091417461792,"beauty":0.01739964801038861,"movies":0.021844295292726947,"leisure_sports":0.009329955966575574,"humor":0.058345876185155875,"music":0.04485514027861094,"charity":0.015389966992934849,"fitness":0.0165814233367729,"health_care":0.021527699213594077,"military":0.013034320299285453,"animals":0.020148544771305524,"dance":0.012551060067223207,"parenting":0.023642682461784918,"shopping":0.01413827847825423,"beverages":0.01989591944350184,"higher_education":0.01992083188540363,"crafts":0.005263564354310484,"nutrition":0.008217999185114544,"extreme_sports":0.0046040907095506066,"science":0.011737067154455726,"toys_and_games":0.004699628710404084,"automotive":0.016683389361043143,"other_sports":0.01786744915770121,"politics":0.03622886489314473,"small_business":0.010401117767321753,"environmentalism":0.010210921567875668,"design":0.0062678792518393875,"dating":0.022562492611140666,"cooking":0.01541533277159928,"computers":0.012154950526783446,"local_life":0.01371711611672098,"art":0.012431124811468516,"gaming":0.018048887641435224,"business":0.02347847262822203,"current_events":0.02491274929978587,"consumer_electronics":0.018235434213545867,"reading":0.0182121319626697,"food":0.030091208884950964,"outdoor_recreation":0.006174227335769481,"religion":0.040720771316832355,"marketing":0.010582783498559166,"multimedia":0.032546506041154,"major_sports":0.059709128166831875,"school_life":0.04198742318776386,"family":0.04478017593705101,"travel":0.025614312842226965,"finance":0.020140523235578984,"pop_culture":0.007421613436708357,"fashion":0.0163075822191156}}
```

This service enables you to get insights at an aggregate level based on an audience.  This service will, for example, return the age range for an entire audience, or the aggregate interests for the same audience.

### Data model

field | description
------|------------
enrichments.demographics.account_type| key / value pairs where key is an enumerated account_type, and value is a percentage of population expressed as a double between 0 and 1
enrichments.demographics.birthyear:| key / value pairs where key is a birthyear, and value is a percentage of population expressed as a double between 0 and 1
enrichments.demographics.race:| key / value pairs where key is an enumerated race, and value is a percentage of population expressed as a double between 0 and 1
enrichments.demographics.gender:| key / value pairs where key is an enumerated gender, and value is a percentage of population expressed as a double between 0 and 1
enrichments.psychographics.interests:| key / value pairs where key is an enumerated interest, and value is a percentage of population expressed as a double between 0 and 1
enrichments.psychographics.languages:| key / value pairs where key is an enumerated language, and value is a percentage of population expressed as a double between 0 and 1
enrichments.psychographics.sentiment:| key / value pairs where key is an enumerated sentiment, and value is a percentage of population expressed as a double between 0 and 1
enrichments.extended.marital_status| key / value pairs where key is an enumerated marital_status, and value is a percentage of population expressed as a double between 0 and 1
enrichments.extended.parental_status| key / value pairs where key is an enumerated parental_status, and value is a percentage of population expressed as a double between 0 and 1
enrichments.extended.political_affiliation| key / value pairs where key is an enumerated political_affiliation, and value is a percentage of population expressed as a double between 0 and 1
enrichments.extended.religion| key / value pairs where key is an enumerated religion, and value is a percentage of population expressed as a double between 0 and 1
enrichments.extended.sexual_orientation| key / value pairs where key is an enumerated sexual_orientation, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.dma| top dmas, expressed as a map, where key is a dma identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.city| top cities, expressed as a map, where key is a city identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.state:| top states, expressed as a map, where key is a state identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.utc_offset| top utc_offsets, expressed as a map, where key is a utc_offset identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.time_zone| top time_zones, expressed as a map, where key is a utc_offset identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.metro_area| top metro_areas, expressed as a map, where key is a metro_area identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.continent| top continents, expressed as a map, where key is a continent identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.place.language| top languages, expressed as a map, where key is a ISO language identifier, and value is a percentage of population expressed as a double between 0 and 1
enrichments.posts.hashtags| top hashtags, expressed as a map, where key is a hashtag, and value is a percentage of posts expressed as a double between 0 and 1
enrichments.posts.mentions| top mentioned accounts, expressed as a map, where key is a profile id, and value is a percentage of posts expressed as a double between 0 and 1