# Execute API

The Execute API allows for programmatic, real-time access to some of People Pattern’s most computationally heavy analytics processes.

Execute supports the following services:

- `twitter`

The following endpoints are used to interact with the Execute API.

* `/configuration/{job_type}`

* `/execute?configuration={config_hash}`

* `/status?configuration={config_hash}&execution={exec_id}`

* `/stop?configuration={config_hash}&execution={exec_id}`

* `/resources/{config_hash}/result.json`

## Workflow

The basic workflow is this:

1. Create a job request using the `/configuration` endpoint.

2. Kick off a job using the `/execute` endpoint.

3. Periodically check the status of your job using the `/status` endpoint.

4. Once your job has finished, retrieve the resulting JSON using the `/resources` endpoint.

## Configuration

This is the endpoint used to specify an audience for, and otherwise configure, your jobs.

Basically, you send an HTTP POST request with a job request payload to the configuration endpoint for the job you want to run.

You'll need the following headers in your HTTP request:

`Accept: application/json`

If the body of your POST request is a JSON file:

`Content-Type: application/json`

Or, if the body of your POST request is a CONF file:

`Content-Type: application/hocon`

Each job has a request schema against which the submitted configuration will be validated, described later in this document

<aside class="notice">
When the API finds a request to be invalid, it will return a BAD_REQUEST status code and a swagger document describing proper usage.
</aside>

When submitting a JSON payload, that payload will be evaluated directly for compliance with the request schema.

When submitting a CONF payload, the API supports `include` expressions which allow you to:
 - Specify audiences using the results of other People Pattern APIs.
 - Specify audiences using any Apache Streams Provider class.
 - Reuse or remix previously submitted configurations.

<aside class="notice">
For examples of proper calls to /configuration with and without `include` expressions, see the different Jobs currently available for the Execute API.
</aside>

## Execute

This is the endpoint used to kick off jobs. To start a job, send an HTTP POST request to the execute endpoint for the job you want to run, specifying the configuration to use when launching the job.

### Resource URI

`/execute/{job_type}`

### Json Schema

type                  | schema URL
----------------------|-----------
Execute Response     | [http://apidocs.peoplepattern.com/schemata/ExecuteResponse.json](http://apidocs.peoplepattern.com/schemata/ExecuteResponse.json)

### POST example (json)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/{job_type}?configuration={configuration}"
```
```json
{"configuration": "{configuration}", "execution":12345, "status":"SUBMITTED"}
```

### POST example (hocon)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/{job_type}?configuration={configuration}"
```
```json
{"configuration": "{configuration}", "execution":12345, "status":"SUBMITTED"}
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

### POST example
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Accept: application/json" \
  'https://api.peoplepattern.com/estimate/{job_type}?configuration={configuration}'
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

`/status?configuration={configuration}&execution={execution}`

### Json Schema

type                  | schema URL
----------------------|-----------
Status Request      | [http://apidocs.peoplepattern.com/schemata/StatusRequest.json](http://apidocs.peoplepattern.com/schemata/StatusRequest.json)
Status Response     | [http://apidocs.peoplepattern.com/schemata/StatusResponse.json](http://apidocs.peoplepattern.com/schemata/StatusResponse.json)

### GET example
```shell
curl -X GET -H "Authorization: $MY_TOKEN" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/status?configuration={configuration}&execution={execution}"
```
```json
{"configuration": "{configuration}", "execution":12345, "status":"RUNNING"}
```
```json
{"configuration": "{configuration}", "execution":12345, "status":"FINISHED"}
```

## Result

The Result endpoint used to retrieve the results of a job after the `/status` endpoint indicates that it has finished executing. To retrieve these results, send an HTTP GET request to this endpoint, specifying your job hash. Note that calling this endpoint for a job which has not yet finished will result in an empty response body. The content of an appropriate response will depend on which kind of job is being executed, but will always be in JSON form.

### Resource URI

`/resources/{job_hash}`

### GET example
```shell
curl -X GET -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/resources/{job_hash}"

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

### POST example (json)
```shell
curl  \
  -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/AnalyzePublicProfiles" \
  -d '{"ids":["twitter:116679528","twitter:118710202", "twitter:119772680"]}'
```
### POST example (hocon)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/AnalyzePublicProfiles" \
  -d 'ids = ["twitter:116679528","twitter:118710202", "twitter:119772680"]'
```

### Audience Influencers

To get an Audience Influencers report for one or more users, make an HTTP POST request to the [Audience Influencers endpoint](#resource-uri-audience-influencers).

`/AudienceInfluencers`

#### Json Schema

type                  | schema URL
----------------------|-----------
AudienceInfluencersReportRequest      | [http://apidocs.peoplepattern.com/schemata/AudienceInfluencersReportRequest.json](http://apidocs.peoplepattern.com/schemata/AudienceInfluencersReportRequest.json)
AudienceInfluencersReportResult      | [http://apidocs.peoplepattern.com/schemata/AudienceInfluencersReportResult.json](http://apidocs.peoplepattern.com/schemata/AudienceInfluencersReportResult.json)

### POST example (JSON)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/configuration/AudienceInfluencers" \
  -d '{ "audience": {"items":["twitter:116679527","twitter:118710202", "twitter:119772680"]} }'
```

### POST example (CONF)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/configuration/AudienceInfluencers" \
  -d 'audience.items = ["twitter:116679527","twitter:118710202", "twitter:119772680"]'
```

### Audience Summary

To get an Audience Summary report for a set of users, make an HTTP POST request to the [Audience Summary endpoint](#resource-uri-audience-summary).

`/AudienceSummary`

#### Json Schema

type                  | schema URL
----------------------|-----------
AudienceSummaryReportRequest      | [http://apidocs.peoplepattern.com/schemata/AudienceSummaryReportRequest.json](http://apidocs.peoplepattern.com/schemata/AudienceSummaryReportRequest.json)
AudienceSummaryReportResult      | [http://apidocs.peoplepattern.com/schemata/AudienceSummaryReportResult.json](http://apidocs.peoplepattern.com/schemata/AudienceSummaryReportResult.json)

### POST example (JSON)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/configuration/AudienceSummary" \
  -d '{ "audience": {"items":["twitter:116679527","twitter:118710202", "twitter:119772680"]} }'
```

### POST example (CONF)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/configuration/AudienceSummary" \
  -d 'audience = { include url("https://api.peoplepattern.com/search?queryString=baseball&max_items=5000") }'
```

### POST example (CONF)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/configuration/AudienceSummary" \
  -d 'audience = { include url("https://api.peoplepattern.com/panels/marketing") }'
```

### POST example (CONF)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/configuration/AudienceSummary" \
  -d 'audience = { include "TwitterFollowingProvider?endpoint=followers&max_items=5000" }'
```

### External Influencers

To get an External Influencers report for one or more users, make an HTTP POST request to the [External Influencers endpoint](#resource-uri-external-influencers).

`/ExternalInfluencers`

#### Json Schema

type                  | schema URL
----------------------|-----------
ExternalInfluencersReportRequest      | [http://apidocs.peoplepattern.com/schemata/ExternalInfluencersReportRequest.json](http://apidocs.peoplepattern.com/schemata/ExternalInfluencersReportRequest.json)
ExternalInfluencersReportResult      | [http://apidocs.peoplepattern.com/schemata/ExternalInfluencersReportResult.json](http://apidocs.peoplepattern.com/schemata/ExternalInfluencersReportResult.json)

### POST example (JSON)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/ExternalInfluencers" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'
```

### POST example (CONF)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/ExternalInfluencers" \
  -d 'ids = ["twitter:116679528","twitter:118710202", "twitter:119772680"]'
```

### Follower Breakdown

To get a follower breakdown for one or more users, make an HTTP POST request to the [Follower Breakdown endpoint](#resource-uri-follower-breakdown).

`/FollowerBreakdown`

#### Json Schema

type                  | schema URL
----------------------|-----------
FollowerBreakdownReportRequest      | [http://apidocs.peoplepattern.com/schemata/FollowerBreakdownReportRequest.json](http://apidocs.peoplepattern.com/schemata/FollowerBreakdownReportRequest.json)
FollowerBreakdownReportResult      | [http://apidocs.peoplepattern.com/schemata/FollowerBreakdownReportResult.json](http://apidocs.peoplepattern.com/schemata/FollowerBreakdownReportResult.json)

### POST example (JSON)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/FollowerBreakdown" \
  -d '{"ids":["twitter:116679527"]}'
```

### POST example (CONF)
```shell
curl -X POST -H "Authorization: $MY_TOKEN" \
  -H "Content-type: application/hocon" \
  -H "Accept: application/json" \
  "https://api.peoplepattern.com/execute/FollowerBreakdown" \
  -d 'ids = ["twitter:116679528"]'
```
