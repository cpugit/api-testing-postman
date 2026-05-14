# TC_users — Test Cases: GET Users

**Base URL:** `https://reqres.in/api`  
**Endpoints:** GET /users, GET /users/{id}

---

## GET /users — List Users

### TC-USR-001 — Get list of users on page 2

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users?page=2` |
| Headers | — |
| Body | — |

**Steps:**
1. Send GET request to `/users?page=2`

**Expected result:**
- Status: `200 OK`
- Body contains `page: 2`
- Body contains `data` array with at least 1 user object
- Each user object has fields: `id`, `email`, `first_name`, `last_name`, `avatar`
- Response time < 2000ms

**Actual result:** ✅ Pass

---

### TC-USR-002 — Get list of users on page 1

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users?page=1` |

**Expected result:**
- Status: `200 OK`
- `page` field equals `1`
- `data` array is not empty
- `total` and `total_pages` fields are present

**Actual result:** ✅ Pass

---

### TC-USR-003 — Pagination: page beyond total returns empty data

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users?page=999` |

**Expected result:**
- Status: `200 OK`
- `data` array is empty `[]`

**Actual result:** ✅ Pass  
**Notes:** API returns 200 with empty array, not 404 — valid REST behaviour

---

### TC-USR-004 — Request without page param returns default page

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users` |

**Expected result:**
- Status: `200 OK`
- `page` equals `1` (default)
- `data` array is not empty

**Actual result:** ✅ Pass

---

## GET /users/{id} — Single User

### TC-USR-005 — Get existing user by valid ID

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users/2` |

**Steps:**
1. Send GET request to `/users/2`

**Expected result:**
- Status: `200 OK`
- Body contains `data` object with `id: 2`
- Fields present: `id` (number), `email` (string), `first_name`, `last_name`, `avatar`
- Body contains `support` object with `url` and `text`

**Actual result:** ✅ Pass

---

### TC-USR-006 — Get user with non-existent ID returns 404

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users/999` |

**Expected result:**
- Status: `404 Not Found`
- Body is empty object `{}`

**Actual result:** ✅ Pass

---

### TC-USR-007 — Get user with ID = 0

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users/0` |

**Expected result:**
- Status: `404 Not Found`

**Actual result:** ✅ Pass  
**Notes:** ID 0 is treated as non-existent

---

### TC-USR-008 — Get user with string instead of ID

| Field | Value |
|-------|-------|
| Method | GET |
| URL | `{{base_url}}/users/abc` |

**Expected result:**
- Status: `404 Not Found` or `400 Bad Request`
- No server error (not 500)

**Actual result:** ✅ Pass — returns 404  
**Notes:** API gracefully handles non-numeric ID
