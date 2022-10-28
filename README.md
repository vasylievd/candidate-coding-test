This should be a Spring Boot application.

- Expose one rest endpoint (POST with body `{"query": "???"}` )
- Call to the exposed endpoint should do the following:
  - (O) Validate the request and return Bad Request in case of invalid
  - (M) In the code create and execute a REST request to external service/endpoint `https://api.datasearch.elsevier.com/api/v4/search?query={{HERE_COMES_VALUE_FROM_THE_REQUEST}}&repositoryType=NON_ARTICLE_BASED_REPOSITORY&sort=RELEVANCY`
  - (M) In the response find the most recently updated object(1) on the first page
  - (M) Create and send back a response `{"totalRecords": ?, "mostRecentId": "?", "updatedDate": "?"}`
  - (O) Each request is saved into RDB (can be in-memory H2) with following fields: query, requestTimestamp, totalRecords, mostRecentId, updatedDate
  - (O) Write unit tests
  - (!O!) Create one-to-many relation in the DB for the same results received in different requests
- Make an actual call to the exposed endpoint and present the response

Additional notes/resources: </br> 
(0) https://docs.datasearch.elsevier.com/swagger-ui/index.html#  </br>
(1) The response is a JSON array of objects. Find the one with the most recent date in `updatedDate` field. </br>
(2) H2 web console `http://localhost:8080/h2-console` (when application is running)
