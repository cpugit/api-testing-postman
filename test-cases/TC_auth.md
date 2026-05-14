# TC_auth — Test Cases: Login & Register

**Base URL:** `https://reqres.in/api`  
**Method coverage:** POST /login, POST /register

---

## POST /login

### TC-AUTH-001 — Successful login with valid credentials

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/login` |
| Headers | `Content-Type: application/json` |
| Body | `{ "email": "eve.holt@reqres.in", "password": "cityslicka" }` |

**Steps:**
1. Send POST request with valid email and password

**Expected result:**
- Status: `200 OK`
- Body contains field `token` (string, non-empty)

**Actual result:** ✅ Pass  
**Notes:** Token value changes on each request (dynamic)

---

### TC-AUTH-002 — Login without password returns 400

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/login` |
| Body | `{ "email": "eve.holt@reqres.in" }` |

**Expected result:**
- Status: `400 Bad Request`
- Body: `{ "error": "Missing password" }`

**Actual result:** ✅ Pass

---

### TC-AUTH-003 — Login without email returns 400

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/login` |
| Body | `{ "password": "cityslicka" }` |

**Expected result:**
- Status: `400 Bad Request`
- Body: `{ "error": "Missing email or username" }`

**Actual result:** ✅ Pass

---

### TC-AUTH-004 — Login with empty body returns 400

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/login` |
| Body | `{}` |

**Expected result:**
- Status: `400 Bad Request`
- Body contains field `error`

**Actual result:** ✅ Pass

---

## POST /register

### TC-REG-001 — Successful registration with valid data

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/register` |
| Body | `{ "email": "eve.holt@reqres.in", "password": "pistol" }` |

**Expected result:**
- Status: `200 OK`
- Body contains: `id` (number), `token` (string)

**Actual result:** ✅ Pass

---

### TC-REG-002 — Register without password returns 400

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/register` |
| Body | `{ "email": "eve.holt@reqres.in" }` |

**Expected result:**
- Status: `400 Bad Request`
- Body: `{ "error": "Missing password" }`

**Actual result:** ✅ Pass

---

### TC-REG-003 — Register with undefined user returns 400

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/register` |
| Body | `{ "email": "newuser@test.com", "password": "12345" }` |

**Expected result:**
- Status: `400 Bad Request`
- Body: `{ "error": "Note: Only defined users succeed registration" }`

**Actual result:** ✅ Pass  
**Notes:** reqres.in only accepts predefined email addresses
