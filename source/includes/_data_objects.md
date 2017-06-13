# Profiles

Profiles are the primary units of information in the PDB.

## JSON Schema

Most requests, responses, and objects have JSON schemas available.

Those types and their schema URLs are introduced throughout the documentation like this:

type                | schema URL
--------------------|-----------
PDB Profile         | [http://apidocs.peoplepattern.com/schemata/pdb-profile.json](http://apidocs.peoplepattern.com/schemata/pdb-profile.json)

PDB Profiles are loosely based on the Activity Streams format, with modest structural changes and many enhancements.

# Enrichments

The structured enrichments appended to profiles include normalized names, aggregated posts, geolocations, demographics, and psychographic attributes.

## JSON Schemas

type                           | schema URL
-------------------------------|-----------
PDB Profile Enrichments        | [http://apidocs.peoplepattern.com/schemata/pdb-profile-enrichments.json](http://apidocs.peoplepattern.com/schemata/pdb-profile-enrichments.json)

### enrichments

field         | type            | description
--------------|-----------------|------------
`account_type`    | enum          | predicted account type of the profile. see [Account Type Vaues](#account-type-values)
`adult`    | boolean          | flag for extreme posting of adult content.
`influence`       | number          | calculated influencer score (0-100) of the profile.
`interestingness` | number          | calculated interestingness score [0-1] of the profile.
`spam`    | boolean          | flag for extreme posting of spam content.

#### Account Type values
- `person`
- `organization`
- `entertainment`

### enrichments.demographics

field         | type            | description
--------------|-----------------|------------
`birthyear`   | number          | predicted or stated birth year of the profile.
`gender`      | string          | predicted gender of the profile. see [Gender values](#gender-values)
`race`        | string          | predicted racial identify of the profile. see [Race values](#race-values)

#### Gender values

- `male`
- `female`

#### Race values

- `white`
- `black`
- `east-asian`
- `south-asian`
- `hispanic`
- `middle-eastern`
- `no-prediction`

<aside class="notice">
Obviously, the values our predictive models use vastly oversimplify
matters of racial and gender identity; the values chosen align roughly
with demographic categories useful for marketing and public relations
use cases, and should not be taken as anything more than that. With
respect to the racial identity categories, our set of values is a
variation of the US Census categories commonly used in media and
marketing analytics, and as such characterize US social media culture
better than other markets.
</aside>

### enrichments.demographics

field         | type            | description
--------------|-----------------|------------
`birthyear`   | number          | predicted or stated birth year of the profile.
`gender`      | string          | predicted gender of the profile. see [Gender values](#gender-values)
`race`        | string          | predicted racial identify of the profile. see [Race values](#race-values)

### enrichments.psychographics
field         | type            | description
--------------|-----------------|------------
`interests.*`   | map           | percentage of posts per tagged interests. see [Interest values](#interests-values)
`languages.*`   | map           | percentage of posts per ISO language code.
`sentiment.*`   | map           | percentage of posts per sentiment classification. see [Sentiment values](#sentiment-values)
`top_interests` | array[string] | array of top 20 interests. see [Interestvalues](#interests-values)
`top_languages` | array[string] | array of top 20 ISO language code.

### enrichments.place

field           | type            | description
----------------|-----------------|------------
`city`          | boolean         | true if the place is a city location
`state`         | boolean         | true if the place is a state location
`province`      | boolean         | true if the place is a province location
`country`       | boolean         | true if the place is a country location
`type`          | string          | "City", "State", "Provice" or "Country"
`geo_name_id`   | number          | the ID number of the place in the Geonames DB
`location`      | [location](#location) | the location record

### enrichments.place.location

field               | type            | description
--------------------|-----------------|------------
`dma`               | string          | the designated market area of the location, if applicable
`city`              | string          | the city name of the location, if applicable
`state`             | string          | the state name of the location, if applicable
`state_abbreviation`| string          | the state abbreviation, if applicable
`utc_offset`        | string          | the UTC offset in minutes, e.g. "-18000" is Eastern Standard
`time_zone`         | string          | the timezone name, if applicable
`metro_area`        | string          | the metropolitan area, if applicable
`continent`         | string          | the continent of the location, if applicable
`language`          | string          | ISO language code of the country of the location
`population`        | number          | population of the location, if applicable
`place_type`        | string          | "City", "State", "Provice" or "Country"
`country`           | string          | the country of the location
`country_code`      | string          | the country code of the location
`coordinates`       | [coordinates](#coordinates) | Lat/long coordinates

### enrichments.place.location.coordinates

field               | type   
--------------------|--------
`latitude`          | number
`longitude`         | number

### enrichments.vcard

field           | type            | description
----------------|-----------------|------------
`name`          | [enrichments.vcard.name](#vcard-name)  | name
`email`         | array of string | emails
`tel`           | array of string | telephone numbers

#### enrichments.vcard.name

field           | type            | description
----------------|-----------------|------------
`given_name`    | string          | given or first name
`family_name`   | string          | family name, surname or last name
`fn`            | string          | full name for display

### posts

field           | type            | description
----------------|-----------------|------------
`devices.*`     | map           | percentage of posts per device type. see [Device Type values](#device-type-values)
`os.*`          | map           | percentage of posts per operating systems. see [Operating System values](#operating-system-values)
`top_domains`   | array[string] | array of top 20 domains
`top_hashtags`  | array[string] | array of top 20 hashtags
`top_mentions`  | array[string] | array of top 20 hashtags

#### Device Type values

- `desktop`
- `tablet`
- `mobile`
- `automated`
- `unknown`

#### Operating System values

- `ios`
- `android`
- `windows`
- `mac`
- `blackberry`
- `unknown`

#### Interest values

- `animals`
- `art`
- `automotive`
- `beauty`
- `beverages`
- `business`
- `charity`
- `computers`
- `consumer_electronics`
- `cooking`
- `crafts`
- `current_events`
- `dance`
- `dating`
- `design`
- `environmentalism`
- `extreme_sports`
- `family`
- `fashion`
- `finance`
- `fitness`
- `food`
- `gaming`
- `health_care`
- `higher_education`
- `home_and_garden`
- `humor`
- `leisure_sports`
- `local_life`
- `major_sports`
- `marketing`
- `military`
- `movies`
- `multimedia`
- `music`
- `nutrition`
- `other_sports`
- `outdoor_recreation`
- `parenting`
- `politics`
- `pop_culture`
- `reading`
- `religion`
- `school_life`
- `science`
- `shopping`
- `small_business`
- `toys_and_games`
- `travel`
- `tv`

#### Sentiment values

- `positive`
- `negative`
- `neutral`
