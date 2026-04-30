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

Steps: Go to Auth0 dashboard Create Application Type: Machine to Machine

Capture These Values (CRITICAL)

From Auth0:

Domain: https://your-tenant.auth0.com/ Audience: https://my-api

Important Note: “These are your trust anchors. API Gateway w

Lab Tasks (Operator Style)

✅ Task 1 — Deploy both Lambdas Different runtimes (Python + Node) Same IAM role (basic execution)

✅ Task 2 — Create API Gateway Use HTTP API (not REST API) → faster + cheaper Add 2 routes

✅ Task 3 — Test via curl Confirm both endpoints respond

✅ Task 4 — Inspect logs Find request payload Find response payload

✅ Task 5 — Break something (important)

You must:

Remove queryStringParameters
Send bad request
👉 Observe logs + behavior
