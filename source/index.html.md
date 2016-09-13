---
title: People Pattern Insights API

language_tabs:
  - shell: cURL
  - json: Output

toc_footers:
  - "&#169; 2016 People Pattern Corporation"
  - <a href="http://peoplepattern.com">People Pattern Home</a>
  - <a href="https://app.peoplepattern.com/signin">Log in</a>

includes:
  - introduction
  - data_objects
  - enrich_api
  - lookup_api
  - search_api
  - aggregate_api
  - errors

search: true
---

# People Pattern Audience Intelligence API

The People Pattern Audience Intelligence API provides access People Pattern's
audience intelligence and model predictions as well as our Portrait Database (Pdb).
You can query the Pdb directly to retrieve portraits with psychographic and demographic attributes pre-appended, 
or you can submit profile and post data to the API and get it enriched.  These are the same services and machine
learning-based models which we use in the
[People Pattern](http://app.peoplepattern.com) application.

The API described above is stateless, in that we do not
store any data provided by you (the client) for application
functionality -- i.e. the service does not support HTTP PUT,
POST, or DELETE requests, at least in spirit. Rather, the API
provides access to resources we've compiled and maintain.

For the [Lookup](#lookup-api), [Search](#search-api) and
[Aggregate](#aggregate-api) APIs, the resource accessed is the
Pdb itself. For the [Enrich API](#enrich-api), the resource
(or resources) are our compiled predictive models.