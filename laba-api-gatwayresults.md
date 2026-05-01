Okay.... let's do this the painful way.---> “REST API is verbose on purpose. It forces you to understand the plumbing.”

Client → Resource → Method → Integration → Lambda → Logs

What REST API Forces You To Understand

Unlike HTTP API, REST API makes you define:

Resource → path (/python)
Method → HTTP verb (GET)
Integration → backend (Lambda)
Deployment → publish changes
Task 1 — Create REST API

📍 Navigation
AWS Console → API Gateway
Click Create API ---> REST API (NOT HTTP API)
Endpoint Type: Regional
Name: chewbacca-rest-api
Task 2 — Create Resources (Paths)

Create /python
    Click Actions → Create Resource
    Resource Name: python
    Resource Path: /python
Create /node
Same process:
    Resource Name: node
    Path: /node
Task 3 — Create Methods

For /python Select /python Click Actions → Create Method Choose: GET

Integration Integration type: Lambda Function Select: chewbacca-python-lambda Click Save

Repeat for /node Connect to: chewbacca-node-lambda

Task 4 — Lambda Permissions

“Add permission to Lambda?”
Click: OK
Remember: API Gateway must be allowed to invoke Lambda
Task 5 — Deploy API (MOST COMMON POINT of Frustration)

“If you don’t deploy, your API does not exist.”
Click: Actions → Deploy API
Configure:
    Deployment stage: New Stage
    Stage name: prod
Task 6 — Get Invoke URL
https://aew7bfz66j.execute-api.us-west-2.amazonaws.com/prod/python
https://aew7bfz66j.execute-api.us-west-2.amazonaws.com/prod/node



You’ll get: https://<api-id>.execute-api.<region>.amazonaws.com/prod
hhttps://aew7bfz66j.execute-api.us-west-2.amazonaws.com/prod/python
ttps://aew7bfz66j.execute-api.us-west-2.amazonaws.com/prod/node?name=Malgus


Task 7 — Test API

Chewbacca Python: curl "https://.execute-api..amazonaws.com/prod/python?name=Chewbacca" Chewbacca Node: curl "https://.execute-api..amazonaws.com/prod/node?name=Malgus"

Task 8 — Verify Logs Go to CloudWatch Find: /aws/lambda/chewbacca-python-lambda /aws/lambda/chewbacca-node-lambda
<img width="1558" height="667" alt="image" src="https://github.com/user-attachments/assets/c466eabf-0aca-4691-b566-c27c5a1f8d97" />
<img width="1543" height="452" alt="image" src="https://github.com/user-attachments/assets/0654b1c3-9c09-4170-bf39-ca8ec5a08f84" />



HOMEWORK RESULTS##########
Return 3 different names from each Lambda endpoint (6 names total), take screenshots of browser output, and upload to github in repo
<img width="1357" height="447" alt="image" src="https://github.com/user-attachments/assets/53b35ce1-0b44-4b71-b6cf-405093a8d47c" />
https://aew7bfz66j.execute-api.us-west-2.amazonaws.com/prod/python

<img width="1658" height="553" alt="image" src="https://github.com/user-attachments/assets/5bed4455-9f52-43d3-996b-b7154eb08cb3" />
https://aew7bfz66j.execute-api.us-west-2.amazonaws.com/prod/node





