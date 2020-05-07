# REST API 

Spring Boot application with Redis database implementing the following REST API's:
  1. POST
  2. GET
  3. PUT
  4. PATCH
  5. DELETE<br/>For every above mentioned API endpoints, proper status codes are returned when validation check fails.
If a resource at any given API is changed a new ETag value is generated to handle the cache thereby, making it more efficient and saving bandwidth.

## Functionality Implemented for the API's

1. Json Schema Validation
2. E-tag conditional read/ write functionality - Cache Implementation to avoid mid-air collisions.
3.  

