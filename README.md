# 🔌 API Testing — Reqres.in (Postman)

Manual + automated API testing of [Reqres.in](https://reqres.in/) — a free hosted REST API for testing and prototyping.

---

## 📌 About This Repository

This repository contains Postman collections, test cases, and bug reports for REST API testing practice.  
It demonstrates skills in: HTTP methods, status code validation, response body checks, negative testing, and environment variables.

**Base URL:** `https://reqres.in/api`  
**Auth:** API key via header (`x-api-key`) — free key available at reqres.in  
**Tool:** Postman v11

---

## 📁 Repository Structure

```
api-testing-postman/
│
├── collections/
│   └── reqres_collection.json      # Postman collection (export v2.1)
│
├── environments/
│   └── reqres_env.json             # Postman environment (base URL, token)
│
├── test-cases/
│   ├── TC_users.md                 # GET /users, GET /users/{id}
│   ├── TC_auth.md                  # POST /login, POST /register
│   └── TC_crud.md                  # POST / PUT / PATCH / DELETE /users
│
├── bug-reports/
│   └── BUG-001_404-not-found.md    # Example defect found during testing
│
└── README.md
```

---

## 🧪 Test Coverage

### Endpoints Tested

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/users?page=2` | Get list of users (paginated) |
| GET | `/users/{id}` | Get single user by ID |
| GET | `/users/999` | Get non-existent user → 404 |
| POST | `/users` | Create new user |
| PUT | `/users/{id}` | Full update of user |
| PATCH | `/users/{id}` | Partial update of user |
| DELETE | `/users/{id}` | Delete user |
| POST | `/login` | Login with valid credentials |
| POST | `/login` | Login without password → 400 |
| POST | `/register` | Register new user |
| POST | `/register` | Register without password → 400 |

---

### Test Types Applied

- ✅ Status code validation (200, 201, 204, 400, 404)
- ✅ Response body structure check (required fields present)
- ✅ Response data type validation (string, number, email format)
- ✅ Negative testing (missing fields, invalid IDs)
- ✅ Response time check (< 2000ms)

---

## 🚀 How to Run

1. Install [Postman](https://www.postman.com/downloads/)
2. Import the collection: `File → Import → collections/reqres_collection.json`
3. Import the environment: `File → Import → environments/reqres_env.json`
4. Select the `Reqres ENV` environment in the top-right dropdown
5. Open a request and click **Send**, or run the full collection via **Collection Runner**

---

## 📋 Example Test Case

**TC-AUTH-002 — Login without password returns 400**

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/login` |
| Body | `{ "email": "eve.holt@reqres.in" }` |
| Expected status | 400 Bad Request |
| Expected body | `{ "error": "Missing password" }` |
| Result | ✅ Pass |

---

## 🔧 Tools Used

| Tool | Purpose |
|------|---------|
| Postman v11 | API requests, test scripts, collection runner |
| Postman Tests (JS) | Status code & body assertions |
| reqres.in | Free public API for practice |

---

## 👤 Author

**[roman m.]**  
Junior QA Engineer  
📧 2698092@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/#)
