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

## Workflow

The basic workflow is this:

1. Validate a job request using the `/estimate` endpoint.

2. Kick off a job using the `/execute` endpoint.

3. Using the job hash that the above step returns, periodically check the status of your job using the `/status` endpoint.

4. When the status endpoint reports that your job has finished, retrieve the resulting JSON using the `/resources` endpoint.

### Estimate
```shell
curl 'https://api.peoplepattern.com/estimate/{job_type}?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: {application/json} OR {application/hocon}" \
  -H "Accept: application/json" \
  -d '{POST_BODY}'
```
```json
{"runMs":300000,"waitMs":300000}
```
```json
{"errors":["Invalid job type"]}
```
```json
{"errors":["Maximum of 1000 ids may be provided"]}
```
```json
{"runMs":300000,"waitMs":300000,"warnings":["At least 50 ids must be provided"]}
```

### Execute
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

`/execute/{job_type}`

This is the endpoint used to kick off jobs. To start a job, send an HTTP POST request to this endpoint, specifying one of the service_type values enumerated below. You'll need the following headers in your HTTP request:

`Accept: application/json`

If the body of your POST request is a JSON file:

`Content-Type: application/json`

Or, if the body of your POST request is a CONF file:

`Content-Type: application/hocon`

<aside class="notice">
For examples of the POST_BODY see the different Jobs currently available for the Execute API.
</aside>

### Status
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

This is the endpoint used to check the status of jobs you've already started. To check job status, send an HTTP GET request to this endpoint specifying your job hash from the `/execute` endpoint as a URL parameter.

### Result
```shell
curl 'https://api.peoplepattern.com/resources/{job_hash}?access_token=$MY_TOKEN' \
  -X GET \
  -H "Content-type: application/json" \
  -H "Accept: application/json"
```

`/resources/{job_hash}`

This is the endpoint used to retrieve the results of a job after the `/status` endpoint indicates that it has finished executing. To retrieve these results, send an HTTP GET request to this endpoint, specifying your job hash. Note that calling this endpoint for a job which has not yet finished will result in an empty response body. The content of an appropriate response will depend on which kind of job is being executed, but will always be in JSON form.

## Jobs

The jobs listed here represent the current set of reports or analysis the supported by the execute API.

### Analyze Public Profiles
```shell
curl 'https://api.peoplepattern.com/execute/AnalyzePublicProfiles?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679528","twitter:118710202", "twitter:119772680"]}'
```
#### Resource URI analyze-public-profiles

`/AnalyzePublicProfiles`

#### HTTP POST
To run the Analyze Public Profiles stream for one or more users, make an HTTP POST request to the [Analyze Public Profiles endpoint](#resource-uri-analyze-public-profiles).

The body of the POST request may be in either JSON or CONF form.

>If JSON, it should look like this:

```shell
{
  "ids":
    ["twitter:116679528",
    "twitter:118710202",
    "twitter:119772680"]
}
```

>If CONF, it should look like this:

```shell
ids = [
 "twitter:42232950"
]
```

### Audience Influencers
```shell
curl 'https://api.peoplepattern.com/execute/AudienceInfluencers?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'
```
#### Resource URI audience-influencers

`/AudienceInfluencers`

#### HTTP POST
To get an Audience Influencers report for one or more users, make an HTTP POST request to the [Audience Influencers endpoint](#resource-uri-audience-influencers).

The body of the POST request may be in either JSON or CONF form.

>If JSON, it should look like this:

```shell
{
  "ids":["twitter:116679527",
        "twitter:118710202",
        "twitter:119772680"]
}
```

>If CONF, it should look like this:

```shell
ids = [
  "twitter:116679527"
  "twitter:118710202"
  "twitter:119772680"
]
```

### External Influencers
```shell
curl 'https://api.peoplepattern.com/execute/ExternalInfluencers?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'
```
#### Resource URI external-influencers

`/ExternalInfluencers`

#### HTTP POST
To get an Exernal Influencers report for one or more users, make an HTTP POST request to the [External Influencers endpoint](#resource-uri-external-influencers).

The body of the POST request may be in either JSON or CONF form.

>If JSON, it should look like this:

```shell
{
  "ids":["twitter:116679527",
        "twitter:118710202",
        "twitter:119772680"]
}
```

>If CONF, it should look like this:

```shell
ids = [
  "twitter:116679527"
  "twitter:118710202"
  "twitter:119772680"
]
```

### Follower Breakdown
```shell
curl 'https://api.peoplepattern.com/execute/FollowerBreakdown?access_token=$MY_TOKEN' \
  -X POST \
  -H "Content-type: application/json" \
  -H "Accept: application/json" \
  -d '{"ids":["twitter:116679527","twitter:118710202", "twitter:119772680"]}'
```

#### Resource URI

`/FollowerBreakdown`

#### HTTP POST
To get a follower breakdown for one or more users, make an HTTP POST request to the [Follower Breakdown endpoint](#resource-uri-follower-breakdown).

The body of the POST request may be in either JSON or CONF form.

>If JSON, it should look like this:

```shell
{
  "ids":["twitter:116679527",
        "twitter:118710202",
        "twitter:119772680"]
}
```

>If CONF, it should look like this:

```shell
ids = [
  "twitter:116679527"
  "twitter:118710202"
  "twitter:119772680"
]
```
