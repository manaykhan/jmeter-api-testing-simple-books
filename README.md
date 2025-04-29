📘 API Testing with JMeter – Simple Books API
This project demonstrates how I used Apache JMeter to perform API testing on the "Simple Books API". For the sake of better understanding, I have divided the assignment in 2 parts:
✅ Part 1: Manual CRUD operations (POST, GET, PATCH, DELETE)
✅ Part 2: Data-driven POST + GET validation using a CSV file


📁 Repository Structure
├── API Test Thread Group.jmx         # Part 1 - Contains POST, GET, PATCH, DELETE flow for a single hardcoded order
├── API Test Thread Group CSV.jmx     # Part 2 - Contains data-driven test (POST + GET) using CSV input
├── orders.csv                  # CSV file with sample data for part 2
└── README.md                   # This file

🔐 API Authentication – Bearer Token
The Simple Books API requires authentication for most endpoints (POST, PATCH, DELETE, etc.).

**How I Registered the API Client**
1. Used Postman to make a request to the following endpoint:
POST https://simple-books-api.glitch.me/api-clients/
**Body**
{
  "clientName": "Mahnoor",
  "clientEmail": "mahnoor.khan0710@gmail.com"
}

2. Received an access token in the response, like this:
{
    "accessToken": "AN_ACCESS_TOKEN"
}

3. Set Authorization header in JMeter via HTTP Header Manager:
Key: Authorization
Value: Bearer <MY_TOKEN>

✅ Part 1: Full API Workflow Test Plan

✔️ File: API Test Thread Group.jmx

This test plan simulates a complete end-to-end flow:
1. POST Order – Creates an order
2. GET Order – Retrieves the same order
3. PATCH Order – Updates the customerName of that order
4. DELETE Order – Deletes the order
5. GET Order After Delete – Confirms deletion by expecting a 404 response

Each request has:
Proper headers set (Content-Type: application/json, Authorization)
JSON Extractor to capture orderId

✅ Part 2: CSV-Driven POST + GET Verification
✔️ File: API Test Thread Group CSV.jmx
This test plan performs data-driven API testing using CSV Data Set Config and a sample orders.csv file.

**Workflow:**
1. Looped POST Requests:
For each row in the CSV, send a POST /orders request
Extract and store the orderId from the response
2. GET Order by orderId:
Use the extracted orderId to call GET /orders/:orderId
Assert that the returned customerName matches the one from the CSV

🚀 How to Run
Open JMeter.
Load API Test Thread Group.jmx or API Test Thread Group CSV.jmx.
Adjust CSV Data Set Config file path if needed.
Run the test.
Inspect results using:
View Results Tree
View Results in Table
Response Assertion

🧠 Summary
This assignment demonstrates my understanding of:
REST API structure and authentication
JMeter threading, samplers, listeners, and assertions
JSON extraction and dynamic variable usage
Data-driven testing via CSV integration
Clean separation of test logic across two plans for clarity and reuse
