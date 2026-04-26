# 🏢 Vantus ERP — Real Estate Management MVP

A full-stack Real Estate ERP system built with the **MERN** stack.

* **Frontend:** Vite + React + TypeScript + Tailwind + Feature-Sliced Design (FSD)
* **Backend:** Node.js + Express + MongoDB (Mongoose) — Modular Monolith
* **Auth:** JWT + Role-Based Access Control (RBAC)
* **Mock payments / notifications** (no real third-party integration in v1)

---

## 📦 Project Structure

```
Erp_Demo/
├── backend/         # Modular monolith API
└── frontend/        # React + FSD SPA
```

---

## 🚀 Quick Start

### 1. Prerequisites
* Node.js ≥ 18
* MongoDB running locally (`mongodb://127.0.0.1:27017`) or any Mongo URI

### 2. Backend
```bash
cd backend
cp .env.example .env
npm install
npm run seed     # populates demo data
npm run dev
```
API runs on `http://localhost:5000/api`.

### 3. Frontend
```bash
cd frontend
npm install
npm run dev
```
App runs on `http://localhost:5173`.

### 4. Demo accounts (after seeding)
| Role        | Email                      | Password   |
|-------------|----------------------------|------------|
| Super Admin | `admin@vantus.com`         | `admin123` |
| Manager     | `manager@vantus.com`       | `manager123` |
| Accountant  | `accountant@vantus.com`    | `accountant123` |
| Agent       | `agent@vantus.com`         | `agent123` |

---

## 🧱 Modules Implemented (MVP)

Properties · Owners · Tenants · Management Contracts · Tenancy Contracts · Rent (invoices + payments) · Expenses · Maintenance · Accounting (P&L, Owner Settlement, Commission) · CRM Leads · Dashboard · User Management & RBAC · Documents · Notifications.

---

## 🔄 Real ERP Workflow

```
Owner → Property → Management Contract
     → Tenancy Contract (Tenant assigned)
     → Rent Invoices auto-generated per period
     → Payments recorded → Income posted
     → Expenses recorded
     → Accounting auto-computes Property P&L
     → Commission deducted → Owner Statement generated
     → Owner Payout marked Paid
```

All payments are **mocked** (cash / cheque / mock-gateway) but the accounting flow is real double-bookkeeping-style.

---

## 🛠 Architecture

### Backend (Modular Monolith)
Each business capability lives in `backend/src/modules/<name>/` with its own model / service / controller / routes. Cross-module logic flows through service-to-service calls only — never direct DB access.

### Frontend (Feature-Sliced Design)
```
src/
├── app/        # providers, routing, global styles
├── pages/      # route-level compositions
├── widgets/    # large, page-section reusables (sidebar, KPI cards…)
├── features/   # user-facing actions (CollectRent, CreateContract…)
├── entities/   # business entities (property, tenant, invoice…)
└── shared/     # UI kit, api client, hooks, lib
```

Imports flow strictly **down** the layer order: `app → pages → widgets → features → entities → shared`.
# Erp_system-
