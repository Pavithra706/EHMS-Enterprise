# Billing & Insurance Management System (BIMS)

## Document Information

| Field | Value |
|--------|--------|
| Project | Enterprise Hospital Management System (EHMS) |
| Phase | Phase 01 – Enterprise Functional Specification |
| Module | Billing & Insurance Management System |
| Version | 2.0 |
| Status | Draft |
| Author | Pavithra K V |

---

# 1. Purpose

The Billing & Insurance Management System (BIMS) manages the complete financial lifecycle of patient care, including charge capture, invoicing, insurance processing, claims management, payment collection, refunds, and financial reporting while ensuring transparency, regulatory compliance, and integration with all hospital services.

---

# 2. Business Objective

The Billing & Insurance module aims to:

- Automate hospital billing.
- Eliminate manual calculation errors.
- Support multiple payment modes.
- Manage insurance pre-authorizations.
- Process insurance claims.
- Improve revenue collection.
- Maintain financial transparency.
- Integrate with all clinical modules.

---

# 3. Scope

The workflow covers:

- OPD Billing
- IPD Billing
- Emergency Billing
- Pharmacy Billing
- Laboratory Billing
- Radiology Billing
- OT Billing
- Blood Bank Billing
- Insurance Management
- Claim Processing
- Refund Management
- Financial Reporting

---

# 4. Actors

## Primary

- Patient
- Billing Executive
- Cashier
- Insurance Executive

## Secondary

- Doctor
- Receptionist
- Finance Officer

## System

- EHMS
- Billing Service
- Insurance Service
- Payment Gateway
- Notification Service
- EHR Service
- Analytics Service

---

# 5. Preconditions

- Patient registered.
- Hospital service provided.
- Charge master configured.
- Insurance details available (if applicable).
- Billing system online.

---

# 6. Main Workflow

## Step 1 – Charge Capture

Charges automatically generated from:

- Registration
- Consultation
- Admission
- Laboratory
- Radiology
- Pharmacy
- OT
- ICU
- Blood Bank
- Procedures
- Bed Charges
- Nursing Charges
- Consumables

↓

Billing Queue Updated

---

## Step 2 – Bill Generation

System calculates:

- Service Charges
- Discounts
- Taxes
- Package Pricing
- Insurance Coverage
- Co-payment
- Patient Payable Amount

↓

Invoice Generated

---

## Step 3 – Insurance Verification

Verify:

- Policy Validity
- Coverage
- Network Hospital
- Pre-Authorization
- Coverage Limits

↓

Insurance Status Updated

---

## Step 4 – Payment Processing

Supported Payments:

- Cash
- Credit Card
- Debit Card
- UPI
- Net Banking
- Insurance
- Corporate Credit
- Digital Wallets

↓

Receipt Generated

---

## Step 5 – Claim Processing

Insurance Claim Created

↓

Documents Uploaded

↓

Claim Submitted

↓

Insurance Review

↓

Approval / Rejection

↓

Settlement

---

## Step 6 – Refund Processing

Applicable for:

- Cancelled Procedures
- Duplicate Payments
- Excess Deposits

↓

Approval Workflow

↓

Refund Processed

---

## Step 7 – Financial Closure

Invoice Closed

↓

Ledger Updated

↓

Finance Reports Updated

↓

Patient EHR Updated

---

# 7. Workflow State Machine

PENDING

↓

GENERATED

↓

VERIFIED

↓

PAID

↓

CLAIM_SUBMITTED

↓

CLAIM_APPROVED

↓

SETTLED

↓

CLOSED

---

# 8. Event Flow

Clinical Services

↓

Billing Service

↓

Insurance Service

↓

Payment Gateway

↓

Finance Service

↓

Notification Service

↓

Analytics Service

↓

EHR Service

---

# 9. Alternative Workflows

- Cash Billing
- Insurance Billing
- Corporate Billing
- Credit Billing
- Emergency Billing
- Package Billing
- Installment Payment

---

# 10. Exception Handling

BIL-EX-001

Insurance Rejected

↓

Patient Self Payment

---

BIL-EX-002

Payment Failed

↓

Retry

↓

Alternative Payment

---

BIL-EX-003

Duplicate Payment

↓

Refund

---

BIL-EX-004

Incorrect Charges

↓

Supervisor Approval

↓

Correction

---

# 11. Business Rules

BIL-BR-001

Every service generates charges.

---

BIL-BR-002

Insurance requires policy verification.

---

BIL-BR-003

Refunds require approval.

---

BIL-BR-004

Invoices cannot be modified after closure.

---

BIL-BR-005

Financial transactions require audit logs.

---

# 12. Business Validation Rules

- Patient exists.
- Services completed.
- Charges valid.
- Insurance active.
- Payment successful.

---

# 13. Error Codes

BIL001 Invalid Invoice

BIL002 Insurance Rejected

BIL003 Payment Failed

BIL004 Duplicate Payment

BIL005 Refund Failed

---

# 14. Notifications

- Bill Generated
- Payment Successful
- Payment Failed
- Insurance Approved
- Insurance Rejected
- Claim Submitted
- Claim Settled
- Refund Processed

---

# 15. Integration Points

- OPD
- IPD
- Emergency
- OT
- Laboratory
- Radiology
- Pharmacy
- Blood Bank
- Inventory
- Finance
- EHR

---

# 16. Database Relationships

Patient

↓

Invoice

↓

InvoiceItem

↓

Payment

↓

InsuranceClaim

↓

Refund

↓

Ledger

---

# 17. Future Database Tables

- Invoice
- InvoiceItem
- Payment
- PaymentMethod
- InsurancePolicy
- InsuranceClaim
- Refund
- Ledger
- FinancialTransaction
- DiscountApproval

---

# 18. REST APIs

POST /billing/invoices

GET /billing/invoices/{id}

POST /payments

POST /insurance/claims

GET /insurance/claims/{id}

POST /refunds

GET /ledger

---

# 19. UI Screens

- Billing Dashboard
- Cash Counter
- Invoice Management
- Payment Screen
- Insurance Dashboard
- Claims Management
- Refund Dashboard
- Revenue Analytics

---

# 20. RBAC Matrix

| Role | Permission |
|------|------------|
| Billing Executive | Create invoices |
| Cashier | Receive payments |
| Insurance Executive | Process claims |
| Finance Manager | Financial reports |
| Administrator | Full access |

---

# 21. Audit Logs

- Invoice Created
- Payment Received
- Claim Submitted
- Claim Approved
- Refund Processed
- Invoice Closed

---

# 22. KPIs

- Daily Revenue
- Collection Rate
- Insurance Approval Rate
- Claim Turnaround Time
- Outstanding Payments
- Refund Rate
- Average Billing Time

---

# 23. SLA

OPD Bill ≤ 3 min

Emergency Bill ≤ 2 min

Insurance Verification ≤ 15 min

Refund ≤ 3 Business Days

---

# 24. Future AI Features

- Revenue Forecasting
- Fraud Detection
- Claim Approval Prediction
- Payment Default Prediction
- Dynamic Revenue Analytics

---

# 25. Healthcare Standards

- HL7 FHIR Claim
- HL7 FHIR Coverage
- ICD-10
- CPT
- SNOMED CT

---

# 26. Microservice Mapping

Primary

↓

billing-service

Connected Services

↓

insurance-service

↓

payment-service

↓

notification-service

↓

analytics-service

↓

ehr-service

↓

patient-service

---

# 27. Security

- Role-Based Access Control
- End-to-End Encryption
- Digital Receipts
- Audit Logs
- Financial Compliance
- Secure Payment Gateway

---

# 28. Approval

| Role | Status |
|------|--------|
| Finance Manager | Pending |
| Insurance Manager | Pending |
| Chief Financial Officer | Pending |
| Hospital Administrator | Pending |
| System Architect | Pending |