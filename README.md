This should be a Spring Boot application.

- Expose one rest endpoint (POST with body `{"query": "???"}` )
- Call to the exposed endpoint should do the following:
  - (O) Validate the request and return Bad Request in case of invalid
  - (M) Create and execute the request to `https://api.datasearch.elsevier.com/api/v4/search?query=whatever&repositoryType=NON_ARTICLE_BASED_REPOSITORY&sort=RELEVANCY`
  - (M) Find the most recently published object on the first page
  - (M) Create and send back a response `{"totalRecords": ?, "mostRecentId": "?", "publicationDate": "?"}`
  - (O) Each request is saved into RDB (can be in-memory H2) with following fields: query, requestTimestamp, totalRecords, mostRecentId, publicationDate
  - (O) Write unit tests
  - (!O!) Create one-to-many relation in the DB for the same results received in different requests
- Make an actual call to the exposed endpoint and present the response
