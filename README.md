# Master
master node 
_SERVICE master:
go to master folder 
run:
docker-compose up // up service to port 8083
for test open url in browesr localhost with port or docker container ip
localhost:8083

you can access api from masterapache

for query to database use api address below
masterapache/cloud/public/api/master/query

params : token
		 query
		 
for vote use api address below
masterapache/cloud/public/api/master/vote

params : token
		 fbid
		 voterId
		 candidateId
		 
you must send valid token to master with name token


finish




Note
----

The voting application only accepts one vote per client. It does not register votes if a vote has already been submitted from a client.I
In the next step user fills out election form and election portal should validate user inputs and send information to the Master Service. this information should contain user token, elections, and user inputs and election portal id.
Master node uses Fraud Detection Service to validates user votes and if it's valid, save vote to the database and update statistic values of each election.
In summary: Panel’s use case: 
Sign up, login, generate token, show statistic to the admin user and add new election to system by admin user
Monitoring’s (Optional) use case: 
Show count of Election Portal tasks  
Show resource load of each task

 Load balancer use case: proxy's user to an election portal
 Master use case:  save elections , present list of available elections , save user votes , update election statistics

First of all user should login or sing up to application ,panel service  dispatch its user to authentication service  and return JSON Web Tokens as result then verified user can vote.
 all users vote send to load balancer service and it send these vote to  election  portals for counting   so that can handle many users that vote in the same time in sperate containers , the result of all counted vote from each election portal service send to master micro service to collect, in this micro service fraud detection check that one person only  vote once  and identity of user are acceptable , result of all election send to database in this micro service  database , authentication, fraud detection and maser service run. Load balancer and election service runs in one container. All of communication in these micro service and container accrued in restful API except in master service with authentication and fraud detection service that send and receive data in Remote Procedure Call (RPC) .   
Eventually election result save in database beside all verified user login details.
  
