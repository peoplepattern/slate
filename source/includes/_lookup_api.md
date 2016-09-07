# Lookup API

## Look up single profile

### GET pattern

```shell
curl 'https://api.peoplepattern.com/pdb/lookup?id=twitter:14132201' \
  -H "Authorization: secretkey" \
  -H'Accept: application/json' 
```

```http
GET /pdb/lookup?id=twitter:14132201 HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey
```

> Response will look like:

```shell
{"enrichments":{"demographics":{"gender":"male","race":"east-asian","birthyear":1985},"vcard":{"name":{"fn":"Kenneth Cho"}},"account_type":"person","version":"0.10","interestingness":0.977957927320845},"$schema":"http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json","twitter":{"statuses_count":1995,"followers_count":2162,"friends_count":1905,"lang":"en","screen_name":"chonuff","favourites_count":375,"listed_count":132},"displayName":"Kenneth Cho","screenName":"chonuff","image":{"url":"http://pbs.twimg.com/profile_images/3496867607/e586594c7088c18b423c19716275859b_normal.jpeg"},"objectType":"profile","createdAt":"2016-03-16T18:03:20.429Z","id":"twitter:14132201","displayScreenName":"chonuff","updatedAt":"2016-03-16T18:03:20.429Z","summary":"Co-founder of @PeoplePattern & @Spredfast. Father of 2 bon vivants. Played college ball & the clarinet.","indexedAt":"2015-11-04T05:24:24.739Z","provider":{"id":"twitter"},"published":"2016-03-16T18:03:20.429Z","url":"http://t.co/iedzuEKtSM","location":"Austin"}
```

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1088

{"enrichments":{"demographics":{"gender":"male","race":"east-asian","birthyear":1985},"vcard":{"name":{"fn":"Kenneth Cho"}},"account_type":"person","version":"0.10","interestingness":0.977957927320845},"$schema":"http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json","twitter":{"statuses_count":1995,"followers_count":2162,"friends_count":1905,"lang":"en","screen_name":"chonuff","favourites_count":375,"listed_count":132},"displayName":"Kenneth Cho","screenName":"chonuff","image":{"url":"http://pbs.twimg.com/profile_images/3496867607/e586594c7088c18b423c19716275859b_normal.jpeg"},"objectType":"profile","createdAt":"2016-03-16T18:03:20.429Z","id":"twitter:14132201","displayScreenName":"chonuff","updatedAt":"2016-03-16T18:03:20.429Z","summary":"Co-founder of @PeoplePattern & @Spredfast. Father of 2 bon vivants. Played college ball & the clarinet.","indexedAt":"2015-11-04T05:24:24.739Z","provider":{"id":"twitter"},"published":"2016-03-16T18:03:20.429Z","url":"http://t.co/iedzuEKtSM","location":"Austin"}
```

Retrieve a single profile from the Lookup API by query a social
profile identifier. Social profile identifiers are of the form

    <service>:<id>
    
For example:

    twitter:1234567
    
Our currently supported services are

- `twitter`
- `instagram`

