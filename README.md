# REST API & Elastc Search Using Kibana

Spring Boot application with Redis database implementing the following REST API's:

1. POST
2. GET
3. PUT
4. PATCH
5. DELETE

For every above mentioned API endpoints, proper status codes are returned when validation check fails.
If a resource at any given API is changed a new ETag value is generated to handle the **cache** thereby, making it more *efficient and saving bandwidth*.

Elastic Search is implmenetd because of its high scalability and *NOSQLDB* property. It uses JSON document files and structure based documents instead of tables and schema.

For specific to this project:-

The key-value pairs generated in the *Redis* server is popped and pushed to a *bytes[]* and then converted to a JSON Object and queued to *restHighLevelClient* pointed to the elastic search server port 9200.
```plan_index``` serves as the index(reference point) of documents with similar characteristics.

## Technology Stack & Resources Used

* [Redis](https://redis.io/) Database - Open source in memory data structure.
* [Elastic Search](https://www.elastic.co/elasticsearch/) - Helps in performing structured unstructured and combined searches.
* [Kibana](https://www.elastic.co/downloads/kibana)- Elastic search tool that is used to query search against the application
* [OAuth 2.0](https://developer.okta.com/blog/2017/06/21/what-the-heck-is-oauth) - OAuth 2.0 token is generated to provide *secure delegated access*. It authorizes the User and delivers proof of authorization. Token is restricted to only access what the User authorized for the specific App.
* [E-tag](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag) - conditional read/ write functionality - Cache Implementation to avoid *mid-air collisions*.
* [Queueing Mechanism](https://www.elastic.co/guide/en/logstash/current/persistent-queues.html) -  *Index Queueing* mechanism is implemented to send request to elastic search from the REST API endpoints
* [Spring Boot](https://www.tutorialspoint.com/spring_boot/spring_boot_introduction.htm) - Spring Boot application developed to implement the Rest API's.

## Steps To Execute

1. Start the elastis search server and verify if it working properly at port 9200
2. Start the redis server at 6379
3. Run the application and verify the api's using [POSTMAN](https://www.postman.com/downloads/) 
4. Generate the OAuth2.0 Token using the ```GET```
```
localhost:8080/token
```
5. ```POST GET``` API is executed and note the ETag value and the plan id generated against.
```
localhost:8080/plan
```
6. ```PUT PATCH``` append the Etag value as well as the plan id generated in Step 5 and run the following api url:-
```
localhost:8080/plan/plan_12xvxc345ssdsds-508
```
Note: After every ``` PUT or PATCH ``` the Etag value is updated.

7. Use multiple queries like below to validate Elastic search query against the application using Kibana.

```
GET /plan_index/_search
{
    "query": {
        "range" : {
            "creationDate" : {
                "gte" : 2014,
                "lte" : 2020,
            }
        }
    }
}
```

