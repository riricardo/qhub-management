# QHub Management Platform

## Overview
QHub Management is a multi-tenant Service Order Management platform designed to manage the complete lifecycle of service requests — from incident creation to execution, billing, and analytics.

The platform is built to support multiple companies (tenants) with strict data isolation, auditability, and scalability.

---

## Core Business Flow
1. Client creates an Incident (Web or WhatsApp)
2. Manager reviews the Incident
3. Manager creates a Budget
4. Client approves the Budget
5. Incident is converted into a Service Order
6. Service Order is executed and finalized
7. Billing and Payments are generated
8. Indicators are updated in the Dashboard

---

## User Roles
- **Administrator** – Full system access across all tenants
- **Manager** – Manages operations within a tenant
- **Employee** – Executes assigned service orders
- **Client** – Requests services and tracks progress

---

## Architecture Overview
- Multi-tenant architecture (single codebase, shared database with tenant isolation)
- Role-Based Access Control (RBAC)
- Centralized audit logging
- Event-driven notifications

---

## Technology Stack

### Frontend
- React
- Mobile-first responsive design

### Backend
- Node.js
- REST APIs
- PostgreSQL

### Integrations
- WhatsApp Business API
- Email (SMTP / provider)
- Stripe or Mercado Pago
- Firebase Auth
- Firebase Storage

### DevOps
- CI/CD pipelines
- Firebase Hosting (Frontend)
- Render (Backend APIs)

---

## Compliance & Security
- GDPR compliant
- Explicit consent tracking
- Data anonymization and deletion
- Audit logs for all critical actions

---

## Project Status
This repository contains:
- A complete and validated backlog
- Clearly defined milestones
- Production-ready product vision
