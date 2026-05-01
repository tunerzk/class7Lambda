JWT Authentication — API Gateway

“Right now, your API is public. Anyone on the internet can hit it. JWT adds identity to every request.”

🎯 Objective: Protect your API so that:

    Only requests with a valid JWT token are allowed
    Unauthorized requests are rejected (401)
    Lambda is only executed if authentication passes

🔑 What is JWT (simple + operator framing)

A JWT is:

    A signed token
    Contains identity (user, claims)
    Verified by API Gateway before Lambda runs

🔁 New Request Flow: Client → API Gateway (JWT Check) → Lambda → Logs

👉 Important Limitation: If JWT fails → Lambda is NEVER called

🧱 Task Flow Overview

We will:

    Create a JWT issuer (Auth0) (fastest for lab)
    Configure JWT Authorizer in API Gateway
    Attach authorizer to routes
    Test with and without token

⚙️ Task 1 — Create JWT Issuer (Auth0)

Use: Auth0

Steps:
    Go to Auth0 dashboard
    Create Application
    Type: Machine to Machine

Capture These Values (CRITICAL)

From Auth0:

  Domain: https://your-tenant.auth0.com/
  Audience: https://my-api
  <img width="1549" height="674" alt="image" src="https://github.com/user-attachments/assets/e935beeb-859c-412c-8f85-36555eefa868" />
  <img width="1452" height="605" alt="image" src="https://github.com/user-attachments/assets/602fd6fb-b99a-48f6-beb9-997a830ffa33" />

  ##### Test without token results####
  <img width="1197" height="445" alt="image" src="https://github.com/user-attachments/assets/73f31691-d5db-482f-8840-4a20225bc31d" />
  “Unauthorized” is exactly what should happen when you call the API without a valid JWT.
That means your JWT authorizer is working and your API is protected.

Now we need to confirm the second half:
👉 that calling it WITH your token returns 200 OK.
####### Test with token results######
<img width="1081" height="297" alt="image" src="https://github.com/user-attachments/assets/031ae221-45c9-4a03-b18d-64dfc017c367" />

Auth0 → JWT → API Gateway → Authorizer → Lambda → Response
All green.
That means:

*Your token was accepted
*Your authorizer validated the issuer
*Your authorizer validated the audience
*Your Lambda executed
*API Gateway returned the response
*You’ve completed the full JWT authentication flow.





Important Note: “These are your trust anchors. API Gateway will verify tokens using this.”
