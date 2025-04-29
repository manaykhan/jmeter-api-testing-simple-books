# 📘 API Testing with JMeter – Simple Books API

This project demonstrates how I used **Apache JMeter** to perform API testing on the [Simple Books API](https://simple-books-api.glitch.me/).  
To keep things clear and modular, I’ve divided the assignment into two parts:

- ✅ **Part 1:** Manual CRUD operations (POST, GET, PATCH, DELETE)  
- ✅ **Part 2:** Data-driven POST + GET validation using a CSV file
  
---

## 🔐 API Authentication – Bearer Token

The Simple Books API requires authentication for most endpoints (POST, PATCH, DELETE, etc.).

### 🔑 How I Registered the API Client

1. Sent a POST request via **Postman** to: https://simple-books-api.glitch.me/api-clients/ with the following JSON body:
```
{
  "clientName": "Mahnoor",
  "clientEmail": "mahnoor.khan0710@gmail.com"
}
```

2. Received an access token in the response, like this:
```
{
    "accessToken": "AN_ACCESS_TOKEN"
}
```

3. Set Authorization header in JMeter via HTTP Header Manager:
```
Key: Authorization
Value: Bearer <MY_TOKEN>
```


## ✅ Part 1: Full API Workflow Test Plan

✔️ File: API Test Thread Group.jmx
  
  This test plan simulates a complete end-to-end flow:
  - POST Order – Creates an order
  - GET Order – Retrieves the same order
  - PATCH Order – Updates the customerName of that order
  - DELETE Order – Deletes the order
  - GET Order After Delete – Confirms deletion by expecting a 404 response

Each request has:
Proper headers set (Content-Type: application/json, Authorization)
JSON Extractor to capture orderId

## ✅ Part 2: CSV-Driven POST + GET Verification
✔️ File: API Test Thread Group CSV.jmx
This test plan performs data-driven API testing using CSV Data Set Config and a sample orders.csv file.

**Workflow:**
1. Looped POST Requests:
For each row in the CSV, send a POST /orders request
Extract and store the orderId from the response
2. GET Order by orderId:
Use the extracted orderId to call GET /orders/:orderId
Assert that the returned customerName matches the one from the CSV

# 🚀 How to Run
1. Open **JMeter**.
2. Load either:
   - `API Test Thread Group.jmx` *(for Part 1)*, or
   - `API Test Thread Group CSV.jmx` *(for Part 2)*.
3. (If running Part 2) Adjust the **CSV Data Set Config** file path if needed.
4. Run the test by clicking ▶️.
5. Inspect the results using:
   - **View Results Tree**
   - **View Results in Table**
   - **Response Assertion**

# 🧠 Summary
This assignment demonstrates my understanding of:
REST API structure and authentication
JMeter threading, samplers, listeners, and assertions
JSON extraction and dynamic variable usage
Data-driven testing via CSV integration
Clean separation of test logic across two plans for clarity and reuse
