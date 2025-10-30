# Nexis Biotech — Initiative THICK (internal excerpt)

---

## Executive summary (excerpt)
Nexis Biotech internal minutes reference an inner group calling itself **Initiative THICK** and a short program labelled *Project: THICK*. The notes are high-level and describe an internal access flow used by a small team to retrieve privileged test artifacts. Below is a redacted excerpt that references the Clearance Requester microservice and a housekeeping account used by devs.

---

## Housekeeping account (engineer)

username: leaker_12
password: GHcreds_ctf_12!


## Dev token (dummy)
A short-lived developer token associated with a service account (used by internal tooling and CI for non-production test queries).

## X-Api-Token: NX-DEV-CTF-9F3A-B0C1


Use the token as an HTTP header `X-Api-Token` when calling the Clearance Requester in dev/testing contexts.

---

## Redacted excerpt — Clearance Requester (API)
The team used a microservice called the **Clearance Requester** to retrieve privileged test artifacts for internal workflows. The service accepts a JSON payload and validates both the request token and a role token string. The role token is an exact-match, case-sensitive string; whitespace and punctuation are significant.

**Endpoint (internal/dev host):**

POST http://HOST:8080/api/request_flag
POST /auth/login
POST /reauth.php
GET/POST /project_thick.php


**Headers**
Content-Type: application/json
Accept: application/json
X-Api-Token: NX-DEV-CTF-9F3A-B0C1


### 1. Initial Login

Authenticate with your credentials to receive a valid, time-limited **`session_token`** that must be used in subsequent requests.

* **Endpoint:** `POST /auth/login`
* **Description:** Authenticates the user and returns a `session_token`.
* **Payload (JSON):**

```json
{
  "username": "leaker_12",
  "password": "GHcreds_ctf_12!"
}
```

### 2. Re-authentication (Token Renewal)

Used to refresh an existing, valid session token before it expires.

* **Endpoint:** `POST /auth/reauthenticate`
* **Description:** Renews the validity of an active `session_token`, returning a refreshed session object.
* **Payload (JSON):**

```json
{
  "session_token": "<SESSION_TOKEN>",
  "role": "role: current_role"
}
```
### 3. Status Count

Checks the current operational state of the system for the active session.

* **Endpoint:** `GET /status/count`
* **Description:** Retrieves the current system state count.
* **Query Parameter:** The **`session_token`** must be passed as a query parameter.

### 4. Key Retrieval (Restricted)

This is the primary restricted endpoint for retrieving a key/flag.

* **Endpoint:** `POST /flag/key`
* **Description:** Attempts to retrieve the key/flag. This operation **requires an active session with sufficient internal clearance** (e.g., a specific user role or permission level).
* **Payload (JSON):**

```json
{
  "session_token": "<PUT_TOKEN_HERE>"
}
```


## ROLES

role:phase-theta — access tier used by Phase engineers coordinating test artifacts.

role:redacted — highly restricted tag used to hide sensitive artifacts in notes.

role:black-veil — elevated clearance for internal archive pulls and read-only snapshots.


