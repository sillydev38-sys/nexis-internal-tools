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

**Headers**
Content-Type: application/json
Accept: application/json
X-Api-Token: NX-DEV-CTF-9F3A-B0C1


**Example JSON payload**
```json
{
  "username": "leaker_12",
  "role": "role:phase-theta"
}

## ROLES

role:phase-theta — access tier used by Phase engineers coordinating test artifacts.

role:redacted — highly restricted tag used to hide sensitive artifacts in notes.

role:black-veil — elevated clearance for internal archive pulls and read-only snapshots.


