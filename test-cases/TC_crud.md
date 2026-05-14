# TC_crud — Test Cases: Create / Update / Delete Users

**Base URL:** `https://reqres.in/api`  
**Endpoints:** POST /users, PUT /users/{id}, PATCH /users/{id}, DELETE /users/{id}

---

## POST /users — Create User

### TC-CRUD-001 — Create user with name and job

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/users` |
| Headers | `Content-Type: application/json` |
| Body | `{ "name": "John QA", "job": "QA Engineer" }` |

**Steps:**
1. Send POST request with valid name and job

**Expected result:**
- Status: `201 Created`
- Body contains: `name`, `job`, `id` (string), `createdAt` (ISO datetime)
- `name` value matches request body

**Actual result:** ✅ Pass  
**Notes:** `id` is returned as a string, not a number — worth noting in documentation

---

### TC-CRUD-002 — Create user with only name (no job)

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/users` |
| Body | `{ "name": "Jane QA" }` |

**Expected result:**
- Status: `201 Created`
- Body contains `name` and `id`
- `job` field is absent or null

**Actual result:** ✅ Pass

---

### TC-CRUD-003 — Create user with empty body

| Field | Value |
|-------|-------|
| Method | POST |
| URL | `{{base_url}}/users` |
| Body | `{}` |

**Expected result:**
- Status: `201 Created`
- Body contains `id` and `createdAt`

**Actual result:** ✅ Pass  
**Notes:** reqres.in accepts empty body — no validation on required fields (expected for mock API)

---

## PUT /users/{id} — Full Update

### TC-CRUD-004 — Full update of existing user

| Field | Value |
|-------|-------|
| Method | PUT |
| URL | `{{base_url}}/users/2` |
| Headers | `Content-Type: application/json` |
| Body | `{ "name": "John Updated", "job": "Senior QA" }` |

**Steps:**
1. Send PUT request with both name and job fields

**Expected result:**
- Status: `200 OK`
- Body contains: `name`, `job`, `updatedAt`
- `name` equals `"John Updated"`, `job` equals `"Senior QA"`

**Actual result:** ✅ Pass

---

### TC-CRUD-005 — PUT with empty body overwrites all fields

| Field | Value |
|-------|-------|
| Method | PUT |
| URL | `{{base_url}}/users/2` |
| Body | `{}` |

**Expected result:**
- Status: `200 OK`
- Body contains `updatedAt`
- `name` and `job` are absent or null (full replacement)

**Actual result:** ✅ Pass

---

## PATCH /users/{id} — Partial Update

### TC-CRUD-006 — Partial update: change job only

| Field | Value |
|-------|-------|
| Method | PATCH |
| URL | `{{base_url}}/users/2` |
| Headers | `Content-Type: application/json` |
| Body | `{ "job": "Lead QA" }` |

**Steps:**
1. Send PATCH request with only `job` field

**Expected result:**
- Status: `200 OK`
- Body contains `job: "Lead QA"` and `updatedAt`
- Other fields are not changed

**Actual result:** ✅ Pass

---

### TC-CRUD-007 — Partial update: change name only

| Field | Value |
|-------|-------|
| Method | PATCH |
| URL | `{{base_url}}/users/2` |
| Body | `{ "name": "Jane Patched" }` |

**Expected result:**
- Status: `200 OK`
- Body contains `name: "Jane Patched"` and `updatedAt`

**Actual result:** ✅ Pass

---

## DELETE /users/{id} — Delete User

### TC-CRUD-008 — Delete existing user

| Field | Value |
|-------|-------|
| Method | DELETE |
| URL | `{{base_url}}/users/2` |
| Headers | — |
| Body | — |

**Steps:**
1. Send DELETE request to `/users/2`

**Expected result:**
- Status: `204 No Content`
- Response body is empty

**Actual result:** ✅ Pass

---

### TC-CRUD-009 — Delete non-existent user

| Field | Value |
|-------|-------|
| Method | DELETE |
| URL | `{{base_url}}/users/999` |

**Expected result:**
- Status: `204 No Content`
- Response body is empty

**Actual result:** ✅ Pass  
**Notes:** reqres.in returns 204 even for non-existent IDs — typical behaviour for mock APIs. In a real system, 404 would be expected. Worth noting as a test observation.
