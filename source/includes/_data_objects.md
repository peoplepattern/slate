# Data objects

## JSON Schema

Most objects returned by the People Pattern Insights API suite
have JSON schema available

type                | schema URL
--------------------|-----------
PDB profile         | [http://apidocs.peoplepattern.com/pdb-pojo/pdb-profile.json](#)
profile enrichments | [http://apidocs.peoplepattern.com/pdb-pojo/pdb-profile-enrichments.json](#)
post enrichments    | [http://apidocs.peoplepattern.com/pdb-pojo/pdb-post-enrichments.json](#)
profile demographics   | [http://apidocs.peoplepattern.com/pdb-pojo/pdb-profile-demographics.json](#)
profile psychographics | [http://apidocs.peoplepattern.com/pdb-pojo/pdb-profile-psychographics.json](#)
extended demographics  | [http://apidocs.peoplepattern.com/pdb-pojo/pdb-profile-extended.json](#)

## Profile (input)

> Example profile request as JSON

```json
{
  "name":"Joe User",
  "username": "juser",
  "description": "my profile",
  "location": "Boston, USA"
}
```

Profiles are objects containing any of the following fields. These are
provided to the profile [Enrich API](#enrich-api) endpoints

field         | type            | description
--------------|-----------------|------------
`name`        | string          | the "display name" or provided profile name
`handle`      | string          | the screen name of the social profile
`summary`     | string          | the description or summary provided with the profile
`location`    | string          | the text representation of the profile location, which often is provided with the social profile

All fields are optional, but a profile containing *none* of these
fields is considered a bad request.

### Enriched profile

An enriched profile consists of a profile data structure --
all or any of the fields provided in an [input profile](#profile-input),
plus other optional data the client may have provided to the Enrich
API -- together with a "peoplepattern" field containing
[profile enrichments](#profile-enrichments).

field           | type        
----------------|-------------
`name`          | string      
`handle`        | string      
`summary`       | string      
`location`      | string      
`enrichments`   | [profile enrichments](#profile-enrichments)

## Profile enrichments

> Example enrichments as JSON

```json
{
  "account_type": "person",
  "spam": false,
  "adult": false,
  "vcard": {
    "name": {
      "given-name": "Joe",
      "family-name": "User",
      "fn": "Joe User"
    },
    "email": []
  },
  "demographics": {
    "birthyear": 1985,
    "gender": "male",
    "race": "white"
  },
  "place": {
    "city": true,
    "geo_name_id": 4930956,
    "type": "City",
    "location": {
      "dma": "Boston, MA-Manchester, NH",
      "city": "Boston",
      "state": "Massachusetts",
      "state_abbreviation": "MA",
      "utc_offset": "-18000",
      "time_zone": "America/New_York",
      "metro_area": "Boston-Cambridge-Newton, MA-NH",
      "continent": "NA",
      "language": "en",
      "population": 617594,
      "place_type": "City",
      "country": "United States",
      "country_code": "US",
      "coordinates": {
        "longitude": 42.35843,
        "latitude": -71.05977
      }
    }
  }
}
```

The structured enrichments appended to profile data by the API
consist of fields for account type, spam, adult content, vcard
(normalized name), demographics, and normalized location.

### vcard

field           | type            | description
----------------|-----------------|------------
`name`          | [vcard.name](#vcard-name)  | name
`email`         | array of string | emails
`tel`           | array of string | telephone numbers

### vcard.name

field           | type            | description
----------------|-----------------|------------
`given_name`    | string          | given or first name
`family_name`   | string          | family name, surname or last name
`fn`            | string          | full name for display

### demographics

field         | type            | description
--------------|-----------------|------------
`birthyear`   | number          | predicted or stated birth year of the profile
`gender`      | string          | predicted gender of the profile
`race`        | string          | predicted racial identify of the profile

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

#### Account Type values
- `person`
- `organization`
- `entertainment`

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


### place/geo

field           | type            | description
----------------|-----------------|------------
`city`          | boolean         | true if the place is a city location
`state`         | boolean         | true if the place is a state location
`province`      | boolean         | true if the place is a province location
`country`       | boolean         | true if the place is a country location
`type`          | string          | "City", "State", "Provice" or "Country"
`geo_name_id`   | number          | the ID number of the place in the Geonames DB
`location`      | [location](#location) | the location record

### location

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

### coordinates

field               | type   
--------------------|--------
`latitude`          | number
`longitude`         | number

## Post (input)

A social media post or other text may be passed to the Enrich API
as a JSON object with a string-valued `text` field

field      | type
-----------|------
text       | string

JSON objects containing other fields may be used, and other
fields are provided back to the client in
[enriched post output](#enriched-post)

## Post enrichments

> Sample post enrichments as JSON

```json
{
  "interests": [
    "science"
  ],
  "languages": [
    "en"
  ],
  "sentiment": "neutral"
}
```

Post enrichments consist of a set of predicted interest topics,
predicted languages and predicted sentiment

field           | type            | description
----------------|-----------------|-----------------------------------------
interests       | array of string | [interest topics](#interest-topic-values)
languages       | array of string | [ISO 639-1 two letter language codes](https://en.wikipedia.org/wiki/ISO_639-1)
sentiment       | string          | "positive", "negative" or "neutral"

#### Interest topic values

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

### Some pdb profile fields

field                                  | description   
---------------------------------------|--------
`enrichments.account_type`             | type of account.  see [Account Type Vaues](#account-type-values)
`enrichments.demographics.race`        | race.  see [Race Values](#race-values)
`enrichments.demographics.gender`      | gender.  see [Gender values](#gender-values)
`enrichments.place.location.city`      | the identified city for the profile
`posts.devices.*`                      | type of device used to commonly post with
`posts.os.*`                           | type of operating system used to commonly post with
`posts.top_domains`                    | top domains linked to by the user.
`posts.top_interests`                  | top categories of interest for the user.  see [Interest topic values](#interests-topic-values)
`posts.top_hashtags`                   | top hashtags for the user.

## Stitch (input)

Persons are objects containing any of the following fields. These are
provided to the stitch [Stitching API](#stitching-api) endpoints

field         | type            | description
--------------|-----------------|------------
`name`        | string          | the first and last name of the person
`email`       | string          | the person's email address, typically the same one used for the social account(s)
`location`    | string          | the text representation of the person's location

All fields are optional, but a person object containing *none* of these fields is considered a bad request, and the more fields submitted increase the quality of matches returned.
