# Execute API

The Execute API allows for programmatic, real-time access to some of People Pattern’s most computationally heavy analytics processes.

Execute supports the following services:

- `twitter`

The following endpoints are used to interact with the Execute API.

* `/estimate/{job_type}`

* `/execute/{job_type}`

* `/status?execution={job_hash}`

* `/stop?execution={job_hash}`

* `/resources/{job_hash}/result.json`

# Workflow

The basic workflow is this:

1. Validate a job request using the `/estimate` endpoint.

2. Kick off a job using the `/execute` endpoint.

3. Using the job hash that the above step returns, periodically check the status of your job using the `/status` endpoint.

4. When the status endpoint reports that your job has finished, retrieve the resulting JSON using the `/resources` endpoint.

## Execute

This is the endpoint used to kick off jobs. To start a job, send an HTTP POST request to this endpoint, specifying one of the service_type values enumerated below. You'll need the following headers in your HTTP request:

`Accept: application/json`

If the body of your POST request is a JSON file:

`Content-Type: application/json`

Or, if the body of your POST request is a CONF file:

`Content-Type: application/hocon`

<aside class="notice">
For examples of the POST_BODY see the different Jobs currently available for the Execute API.
</aside>

### Resource URI

`/execute/{job_type}`

### Json Schema

type                  | schema URL
----------------------|-----------
Execute Request      | [http://apidocs.peoplepattern.com/schemata/ExecuteRequest.json](http://apidocs.peoplepattern.com/schemata/ExecuteRequest.json)
Execute Response     | [http://apidocs.peoplepattern.com/schemata/ExecuteResponse.json](http://apidocs.peoplepattern.com/schemata/ExecuteResponse.json)

```shell
curl 'https://api.peoplepattern.com/execute/{job_type}?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: {application/json} OR {application/hocon}" \
  -H "Accept: application/json" \
  -d '{POST_BODY}'
```
```json
{"execution":"{job_hash}","status":"SUBMITTED"}
```

## Estimate

Estimate determines whether a job request is valid, and estimates how long the job will take to begin and then to complete execution.

### Resource URI

`/estimate`

### Json Schema

type                  | schema URL
----------------------|-----------
Estimate Request      | [http://apidocs.peoplepattern.com/schemata/EstimateRequest.json](http://apidocs.peoplepattern.com/schemata/EstimateRequest.json)
Estimate Response     | [http://apidocs.peoplepattern.com/schemata/EstimateResponse.json](http://apidocs.peoplepattern.com/schemata/EstimateResponse.json)

The potential errors and warnings returned differ by job type.

```shell
curl 'https://api.peoplepattern.com/estimate/{job_type}?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: {application/json} OR {application/hocon}" \
  -H "Accept: application/json" \
  -d '{POST_BODY}'
```
```json
{"valid": true, "runMs":300000, "waitMs":300000}
```
```json
{"errors":["Invalid job type"]}
```
```json
{"errors":["Maximum of 1000 ids may be provided"]}
```
```json
{"valid": true, "runMs":300000, "waitMs":300000, "warnings":["At least 50 ids must be provided"]}
```
```json
{"valid": false, "errors":["A list of ids must be present"]}
```

## Status

The Status endpoint used to check the status of jobs you've already started. To check job status, send an HTTP GET request to this endpoint specifying your job hash from the `/execute` endpoint as a URL parameter.

### Resource URI

`/status`

### Json Schema

type                  | schema URL
----------------------|-----------
Status Request      | [http://apidocs.peoplepattern.com/schemata/StatusRequest.json](http://apidocs.peoplepattern.com/schemata/StatusRequest.json)
Status Response     | [http://apidocs.peoplepattern.com/schemata/StatusResponse.json](http://apidocs.peoplepattern.com/schemata/StatusResponse.json)

```shell
curl 'https://api.peoplepattern.com/status?execution={job_hash}?access_token=$MY_TOKEN' \
  -X GET \
  -H "Content-type: application/json" \
  -H "Accept: application/json"
```
```json
{"execution":"{job_hash}","status":"RUNNING"}
```
```json
{"execution":"{job_hash}","status":"FINISHED"}
```
`/status?execution={job_hash}`

## Result

The Result endpoint used to retrieve the results of a job after the `/status` endpoint indicates that it has finished executing. To retrieve these results, send an HTTP GET request to this endpoint, specifying your job hash. Note that calling this endpoint for a job which has not yet finished will result in an empty response body. The content of an appropriate response will depend on which kind of job is being executed, but will always be in JSON form.

### Resource URI

`/resources/{job_hash}`

```shell
curl 'https://api.peoplepattern.com/resources/{job_hash}?access_token=$MY_TOKEN' \
  -X GET \
  -H "Content-type: application/json" \
  -H "Accept: application/json"
```

## Jobs

The jobs listed here represent the current set of reports or analysis the supported by the execute API.

### Analyze Public Profiles

To run the Analyze Public Profiles stream for one or more users, make an HTTP POST request to the [Analyze Public Profiles endpoint](#resource-uri-analyze-public-profiles).

`/AnalyzePublicProfiles`

#### Json Schema

type                  | schema URL
----------------------|-----------
AnalyzePublicProfilesRequest      | [http://apidocs.peoplepattern.com/schemata/AnalyzePublicProfilesRequest.json](http://apidocs.peoplepattern.com/schemata/AnalyzePublicProfilesRequest.json)

```shell
curl 'https://api.peoplepattern.com/execute/AnalyzePublicProfiles?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679528","twitter:118710202", "twitter:119772680"]}'

curl 'https://api.peoplepattern.com/execute/AnalyzePublicProfiles?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  -d 'ids = ["twitter:116679528","twitter:118710202", "twitter:119772680"]'
```

### Audience Influencers

To get an Audience Influencers report for one or more users, make an HTTP POST request to the [Audience Influencers endpoint](#resource-uri-audience-influencers).

`/AudienceInfluencers`

#### Json Schema

type                  | schema URL
----------------------|-----------
AudienceInfluencersRequest      | [http://apidocs.peoplepattern.com/schemata/AudienceInfluencersRequest.json](http://apidocs.peoplepattern.com/schemata/AudienceInfluencersRequest.json)
AudienceInfluencersResult      | [http://apidocs.peoplepattern.com/schemata/AudienceInfluencersResult.json](http://apidocs.peoplepattern.com/schemata/AudienceInfluencersResult.json)

```shell
curl 'https://api.peoplepattern.com/execute/AudienceInfluencers?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'

curl 'https://api.peoplepattern.com/execute/AudienceInfluencers?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  -d 'ids = ["twitter:116679528","twitter:118710202", "twitter:119772680"]'
```

### External Influencers

To get an External Influencers report for one or more users, make an HTTP POST request to the [External Influencers endpoint](#resource-uri-external-influencers).

`/ExternalInfluencers`

#### Json Schema

type                  | schema URL
----------------------|-----------
ExternalInfluencersRequest      | [http://apidocs.peoplepattern.com/schemata/ExternalInfluencersRequest.json](http://apidocs.peoplepattern.com/schemata/ExternalInfluencersRequest.json)
ExternalInfluencersResult      | [http://apidocs.peoplepattern.com/schemata/ExternalInfluencersResult.json](http://apidocs.peoplepattern.com/schemata/ExternalInfluencersResult.json)

```shell
curl 'https://api.peoplepattern.com/execute/ExternalInfluencers?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'

curl 'https://api.peoplepattern.com/execute/ExternalInfluencers?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  -d 'ids = ["twitter:116679528","twitter:118710202", "twitter:119772680"]'
```

### Follower Breakdown

To get a follower breakdown for one or more users, make an HTTP POST request to the [Follower Breakdown endpoint](#resource-uri-follower-breakdown).

`/FollowerBreakdown`

#### Json Schema

type                  | schema URL
----------------------|-----------
FollowerBreakdownRequest      | [http://apidocs.peoplepattern.com/schemata/FollowerBreakdownRequest.json](http://apidocs.peoplepattern.com/schemata/FollowerBreakdownRequest.json)
FollowerBreakdownResult      | [http://apidocs.peoplepattern.com/schemata/FollowerBreakdownResult.json](http://apidocs.peoplepattern.com/schemata/FollowerBreakdownResult.json)

```shell
curl 'https://api.peoplepattern.com/execute/FollowerBreakdown?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'
```
