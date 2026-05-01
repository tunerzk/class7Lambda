🛡️ WAF Lab — Protecting API Gateway (ClickOps)

“We are binding protection directly to the front door.”

🎯 Objective

Attach a Web Application Firewall (WAF) to your API so that:

Malicious or suspicious requests are blocked before Lambda
Students see real security controls in action
Logs + behavior reinforce “edge-first security”

🧠 Concept First: “Right now your API trusts everyone. WAF is your first line of defense.”

🔁 Updated Request Flow: Client → WAF → API Gateway → Lambda → Logs
👉 Critical insight: If WAF blocks → API Gateway and Lambda are NEVER reached

🧱 What We’re Building
    WAF Web ACL
    Rules:
        Block obvious bad patterns
        Rate limiting (optional but powerful)
    Attach WAF to API Gateway

⚙️ Task 1 — Create Web ACL
📍 Navigation
AWS Console → WAF & Shield
Click Create Web ACL
<img width="1482" height="700" alt="image" src="https://github.com/user-attachments/assets/41a1e468-9364-43b0-ad6b-84612763301a" />


🛠️ Configuration

        Name: chewbacca-api-waf
        Resource Type:: Regional resources
        Region: 👉 Same region as your API Gateway

Associated Resource:
Select: API Gateway
Choose your API

⚙️ Task 2 — Add Rules

We keep this simple but meaningful.

🧩 Rule 1 — AWS Managed Rule Group
Add rule → Add managed rule groups

Select: AWSManagedRulesCommonRuleSet

This blocks common attacks like:

    SQL injection patterns
    bad headers
    known malicious inputs

🧩 Rule 2 — Rate Limiting (VERY IMPORTANT)
Add rule → Rate-based rule

Configuration:

    Limit: 100 requests per 5 minutes
    Action: Block
<img width="1553" height="515" alt="image" src="https://github.com/user-attachments/assets/931a8192-3961-4b7e-a3cf-fc583dc0dd2a" />


⚙️ Task 3 — Set Default Action

    Default: Allow

Only bad traffic is blocked, everything else flows through

🚀 Task 4 — Create Web ACL


Click Create
<img width="1474" height="575" alt="image" src="https://github.com/user-attachments/assets/dbb5e5e3-1d11-4439-94b0-2d47ea215f2f" />


🔍 Task 5 — Validate Behavior

Now we test like operators.

✅ Normal Request: curl "https://<api-id>/python?name=Chewbacca"
<img width="1481" height="543" alt="image" src="https://github.com/user-attachments/assets/55ff1927-7df9-47ae-886d-5d079612c560" />

XSS ATTACK (SHOULD BLOCK)
curl "https://5e7r148t5c.execute-api.us-west-2.amazonaws.com/prod/python?name=<script>alert(1)</script>"
<img width="1373" height="477" alt="image" src="https://github.com/user-attachments/assets/9f744ceb-1f8a-44df-af0a-f02159529b57" />

SQL INJECTION (SHOULD BLOCK)
curl "https://5e7r148t5c.execute-api.us-west-2.amazonaws.com/prod/python?name=' OR 1=1 --"
<img width="973" height="225" alt="image" src="https://github.com/user-attachments/assets/4f278cfe-320c-4e14-a1dd-adc76142b4c4" />








💥 Task 6 — Trigger WAF Block
Method 1 — Suspicious Input: curl "https://<api-id>/python?name=<script>alert(1)</script>"

👉 Expected: 403 Forbidden (or blocked)

Method 2 — Rate Limit (if you want drama)

Run loop: for i in {1..150}; do curl -s "https://<api-id>/python"; done
<img width="1323" height="340" alt="image" src="https://github.com/user-attachments/assets/cdab66e6-9c8a-4460-81bd-f959494662b0" />


👉 Expected: Eventually blocked

🔍 Task 7 — Verify WAF Logs / Metrics
Go to: WAF → Your Web ACL → Overview
<img width="1497" height="270" alt="image" src="https://github.com/user-attachments/assets/3ef40b7a-c15f-4292-9b6d-feaea8bf9010" />


Look at:
        Allowed requests
        Blocked requests
      <img width="1281" height="451" alt="image" src="https://github.com/user-attachments/assets/599ee92e-d7d4-4b75-b9da-8c5cf80a1237" />
      
  

Test:

1. Where does WAF sit? AWS WAF sits in front of your API Gateway REST API, acting as a protective layer that inspects every incoming request before it reaches your API or Lambda.
   
2. What happens if WAF blocks? When WAF blocks a request, The request never reaches API Gateway, and Your Lambda function never runs. WAF immediately returns a 403 Forbidden. A log entry is written to your WAF log group (aws-waf-logs-chewbacca) and The block is counted in the Web ACL metrics. This protects your backend from malicious or excessive traffic.
   
3. Why is this important? Because WAF provides centralized, automated protection at the edge of your application.
It matters because:
It stops attacks before they hit your API
It reduces load on API Gateway and Lambda
It protects you even if your code has vulnerabilities
It gives visibility into malicious traffic patterns
It enforces rate limits to prevent abuse , WAF is your first line of defense for application‑layer security.
   
4. What kind of attacks does WAF stop?  WAF can block:
Application‑layer attacks
SQL injection
Cross‑site scripting (XSS)
Command injection
Path traversal
Local/remote file inclusion
Malicious or suspicious traffic
Known bad IPs (IP reputation lists)
Botnets and scanners
Automated exploit tools
Abuse and DDoS‑like behavior
High request rates (your rate‑based rule)
Flooding from a single IP
Malformed or dangerous requests
Encoded payloads
Invalid headers
Suspicious query strings
   

“WAF is your bouncer. Lambda is your bartender.”

“If bad traffic reaches Lambda, you already paid for the mistake.”

“Good systems reject early and cheaply.”

🏁 Exit Criteria

Student passes when:

✔ WAF created
✔ Attached to API Gateway
✔ Managed rules active
✔ Rate limit configured
✔ Can trigger a block
✔ Can explain flow





