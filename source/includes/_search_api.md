# Search API

## This service allows you to search the pdb and discover an audience based on a search query

### GET pattern

```shell
curl '/pdb/search?queryString=joe'
  -H "Authorization: secretkey" \
  -H'Accept: application/json' 
```

```http
GET /pdb/search?queryString=joe HTTP/1.1
Host: api.peoplepattern.com
Accept: application/json
Content-type: application/json
Authoriation: secretkey
```

> Response will look like:

```shell
[{"$schema":"http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json","twitter":{"statuses_count":708,"followers_count":48,"friends_count":86,"lang":"en","listed_count":0,"screen_name":"jszulueta","favourites_count":3},"enrichments":{"psychographics":{"languages":{"android":5,"ios":6},"interests":{"business":2,"health_care":3,"military":6,"consumer_electronics":5,"beverages":3,"computers":2,"other_sports":2,"science":3,"crafts":1,"design":3,"religion":3,"shopping":4,"food":6,"local_life":11,"travel":22,"multimedia":52,"family":2,"beauty":1,"environmentalism":2,"humor":4},"sentiment":{"neutral":1,"positive":126},"mentions":["twitter:122302784","twitter:14120151","twitter:2166412230","twitter:960481315","twitter:71983360","twitter:106915372","twitter:14511951","twitter:15092616","twitter:2576461322","twitter:326380075","twitter:347258974","twitter:3746042353","twitter:871351657"],"hashtags":["3d","fps","mobile","pg3d","pixelgun","pixelgun3d","shooter","HiddenRisks","TheSMStoreMakati3DS","WaltDisney","gifersation"]},"demographics":{"race":"white","birthyear":1999,"gender":"female"},"account_type":"person","version":"0.10","vcard":{"name":{"fn":"Joe Zulueta"}},"interestingness":0.8452886615186165},"screenName":"jszulueta","objectType":"profile","id":"twitter:130573602","displayScreenName":"jszulueta","provider":{"id":"twitter"},"published":"2010-04-07T17:56:08.000Z","displayName":"★ joe","image":{"url":"http://pbs.twimg.com/profile_images/491912407841644544/7dD2PrDr_normal.jpeg"},"summary":"joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe","indexedAt":"2015-11-03T23:31:29.870Z","location":"Manila"}]
```

```http
HTTP/1.1 200 OK
Content-Type: application/json
Content-Length: 1088

[{"$schema":"http://streams.peoplepattern.com.s3-website-us-east-1.amazonaws.com/streams-internal/0.3.7-PP-SNAPSHOT/pdb-pojo/pdb-profile.json","twitter":{"statuses_count":708,"followers_count":48,"friends_count":86,"lang":"en","listed_count":0,"screen_name":"jszulueta","favourites_count":3},"enrichments":{"psychographics":{"languages":{"android":5,"ios":6},"interests":{"business":2,"health_care":3,"military":6,"consumer_electronics":5,"beverages":3,"computers":2,"other_sports":2,"science":3,"crafts":1,"design":3,"religion":3,"shopping":4,"food":6,"local_life":11,"travel":22,"multimedia":52,"family":2,"beauty":1,"environmentalism":2,"humor":4},"sentiment":{"neutral":1,"positive":126},"mentions":["twitter:122302784","twitter:14120151","twitter:2166412230","twitter:960481315","twitter:71983360","twitter:106915372","twitter:14511951","twitter:15092616","twitter:2576461322","twitter:326380075","twitter:347258974","twitter:3746042353","twitter:871351657"],"hashtags":["3d","fps","mobile","pg3d","pixelgun","pixelgun3d","shooter","HiddenRisks","TheSMStoreMakati3DS","WaltDisney","gifersation"]},"demographics":{"race":"white","birthyear":1999,"gender":"female"},"account_type":"person","version":"0.10","vcard":{"name":{"fn":"Joe Zulueta"}},"interestingness":0.8452886615186165},"screenName":"jszulueta","objectType":"profile","id":"twitter:130573602","displayScreenName":"jszulueta","provider":{"id":"twitter"},"published":"2010-04-07T17:56:08.000Z","displayName":"★ joe","image":{"url":"http://pbs.twimg.com/profile_images/491912407841644544/7dD2PrDr_normal.jpeg"},"summary":"joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe joe","indexedAt":"2015-11-03T23:31:29.870Z","location":"Manila"}]
```