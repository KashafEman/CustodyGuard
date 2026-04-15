

#  Custody Guard

**A Digital Evidence Chain of Custody Management System**
*By Kashaf Eman*



##  Overview

Custody Guard is a full-stack forensic evidence management system designed to preserve the **integrity, traceability, and authenticity** of digital evidence throughout its lifecycle.

In the world of digital forensics, evidence doesn’t fail loudly—it fails silently. One unnoticed modification, one missing log… and the truth collapses in court.

This system exists to make that collapse impossible.

Custody Guard enforces a **tamper-aware, audit-driven workflow** where every action is tracked, verified, and accountable.



##  Core Objectives

* Preserve **chain of custody integrity**
* Detect and prevent **evidence tampering**
* Enable **transparent forensic workflows**
* Provide **secure, role-based access control**
* Maintain **legally defensible audit trails**



##  Project Architecture

```
                ┌──────────────────────┐
                │     React Frontend   │
                │  (User Interface)    │
                └─────────┬────────────┘
                          │ API Calls (JWT)
                          ▼
                ┌──────────────────────┐
                │     FastAPI Backend  │
                │  (Business Logic)    │
                └─────────┬────────────┘
                          │
        ┌─────────────────┼─────────────────┐
        ▼                 ▼                 ▼
┌──────────────┐  ┌──────────────┐  ┌────────────────┐
│ Database     │  │ Hash Engine  │  │ Audit Logger   │
│ (SQLAlchemy) │  │ (SHA-256)    │  │ (Immutable)    │
└──────────────┘  └──────────────┘  └────────────────┘
```



##  Project Structure

```
demccs/
├── backend/               # FastAPI backend
│   ├── main.py            # Entry point
│   ├── database.py        # DB configuration
│   ├── models.py          # Entities: User, Case, Evidence, AuditLog
│   ├── auth_utils.py      # JWT auth + password hashing
│   ├── requirements.txt
│   └── routers/           # Modular API routes
│       ├── auth.py
│       ├── cases.py
│       ├── evidence.py
│       └── audit.py
│
└── frontend/              # React frontend
    ├── public/
    └── src/
        ├── context/       # Auth state management
        ├── utils/         # API communication
        ├── components/    # Shared UI
        └── pages/         # Application views
```



##  Features

###  Authentication & Authorization

* JWT-based stateless authentication
* Secure password hashing using bcrypt
* Role-based access control:

  * **Admin** → full control
  * **Investigator** → operational access



###  Case Management

* Create and manage investigation cases
* Unique case identifiers for traceability
* Priority levels: High / Medium / Low
* Status lifecycle: Open / Closed / On Hold
* Search and filtering for quick navigation



###  Evidence Management

* Secure file uploads with metadata
* Automatic **MD5 + SHA-256 hashing**
* Structured evidence lifecycle:

  ```
  Acquired → Under Analysis → Awaiting Review → Ready → Archived
  ```
* Controlled and logged file downloads


###  Chain of Custody Tracking

* Every action is recorded:

  * Upload
  * View
  * Download
  * Status updates
* Timestamped + IP-tracked logs
* Append-only audit system (no silent edits)



###  Audit Logging

* Immutable forensic logs
* Case-level and evidence-level tracking
* Designed for legal defensibility



###  Security Design

* JWT-protected API endpoints
* Role-based permission enforcement
* Password encryption via bcrypt
* CORS protection for frontend/backend communication
* HTTPS-ready deployment



##  Technology Stack

| Layer          | Technology              |
| -------------- | ----------------------- |
| Backend        | FastAPI (Python)        |
| Frontend       | React.js                |
| Database       | SQLAlchemy ORM          |
| Authentication | JWT (python-jose)       |
| Security       | bcrypt                  |
| Hashing        | hashlib (MD5 + SHA-256) |



##  How Integrity Verification Works

1. File is uploaded
2. System generates **MD5 + SHA-256 hash**
3. Hash is stored alongside metadata
4. On verification:

   * File is re-hashed
   * Compared with original hash
5. Any mismatch = **tampering detected instantly**



##  Real-World Use Cases

* Digital forensic investigations
* Cybercrime analysis
* Law enforcement evidence tracking
* Corporate security incident response
* Legal compliance & auditing



