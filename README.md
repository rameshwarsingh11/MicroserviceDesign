# MicroserviceDesign

Attaching below items for the two selected microservices : Account balance and Money transfer 

 
1. RAML 

2. Swagger YAML 

Implementation pattern : 
API Gateway. Need to use Zull service for API gateway to mange the APIs including its load balancing, routing, security, scaling and fault tolerance. An representational diagram is attached in the solution.

========================================

Deployment Strategy :

Use Pivotal Cloud foundry.
Below steps to be repeated for successfully managing and deploying the APIs on cloud foundry :
1. Get the product license and install Cloud foundry CLI.
2. Log in to your account in CLI using "cf login" command
3. Create a clear db service instance using this command : cf create-service cleardb spark mysql
4. Configure the manifest.yml file using below sample configs :
---
applications:
  - name: pivotalservice
    buildpack: dbs-dummy
    path: build/libs/dbs-dummy-service-0.0.1-SNAPSHOT.jar
    services:
      - mysql
5. push the microservices jar file using "cf push" command.
6. Check the status of the deployed service.
7. Now you can test your end points.
https://dbs-dummy.com/accountBalance
// This will list out all the account balances of all of your clients.
