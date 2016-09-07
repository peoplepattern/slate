### Overview

The People Pattern API suite enables you to access content from
our person-based dataset (PDB), and enrich your own text and person
data with our models. We break this down into four areas of
functionality:

- [Lookup API](#lookup-api) Look up profile records in the PDB by ID
- [Search API](#search-api) Search for profile records in the PDB by
  certain criteria
- [Summarize API](#summarize-api) Summarize demographic and other
  attributes of profile records in the PDB, either for sets of IDs
  or search criteria
- [Enrich API](#enrich-api) Enrich profile and text data you provide
  with our compiled predictive models

### API Philosophy

Each of the APIs described above is stateless, in that we do not
store any data provided by you (the client) for application
functionality -- i.e. the service does not support HTTP PUT,
POST, or DELETE requests, at least in spirit. Rather, the API
provides access to resources we've compiled and maintain.

For the [Lookup](#lookup-api), [Search](#search-api) and
[Summarize](#summarize-api) APIs, the resource accessed is the
PDB itself. For the [Enrich API](#enrich-api), the resource
(or resources) are our compiled predictive models.