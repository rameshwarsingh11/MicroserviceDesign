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
applications:
  - name: dbs-dummy-service
    buildpack: dbs-dummy
    path: build/libs/dbs-dummy-service-0.0.1-SNAPSHOT.jar
    services:
      - mysql
      
5. push the microservices jar file using "cf push" command.
6. Check the status of the deployed service.
7. Now you can test your end points.
https://dbs-dummy.com/accountBalance

// This will list out all the account balances of all of your clients.

=======================================

Interprocess communication between two APIs :
Use Apache Active MQ and kafka for inter process communication. The data will flow out from one micro service to a queue and read by another micro service. The facilitation between Active MQ and micro service will be done my Apache MQ.

=========================================

Externatilization of API properties :
Deploy the environment specific configs on storm UI and present the path to cloud foundry service discovery . It will load the required properties based on environment.
Deploy the environment specific configs on storm UI and present the path to cloud foundry service discovery . It will load the required properties based on environment.
The folder structure to be used as below :
/config
	-DEV
	-QA
	-STAGE
	-UAT
	-PAT
	-PROD

======================================

Cross cutting concerns on API gateway :
1.	Authentication & Authorization : Use licensed product an identity manager like PINGFED. Onboard all the clients ( consumer applications ) for these API with PingFED. On each service call ping fed will authenticate the clients and provide Oauth 2 token which will contain user id, token expiry, scopes ( authorization ) etc . Using this token the client should be able to make API calls. The authentication of individuation users for page / tab access shall be validated by LDAP service. 

For few clients SAML policy interceptors to be implemented and onboarded accordingly.

2.	Load balancing : Use F5 load balancers to balance the load on different data centers. API gateway will provide the request to these gateways which will further distribute this call to lesser loaded server based on ML algorithms.

3.	Scaling : Z cube scaling paradigm to be leveraged. Based on hardware capabilities horizontal scaling should be done. AWS EC2, Beanstalk shall be used for this purpose.

4.	Performance :
Hazelcaset to be used for caching and in memory db cache and making sure the APIs are not making frequent db / cloud calls for data accumulation and computation.

5.	Fault tolerance and availability :  Cassandra dba follows v node share capabilities to avoid zero downtime and 100% availability. It doesn’t follow the master slave architecture and the v node share pattern does the fault tolerance backups in few microseconds only . This makes the solution highly available and fault tolerant.
6.	Logging : Splunk server to be used for logging purpose. 

7.	Security : Apart from techniques used in point 1, the API itself will need to implement blockchain kind of hashing mechanism to avoid any tempering or hacker attacks.

======================================






