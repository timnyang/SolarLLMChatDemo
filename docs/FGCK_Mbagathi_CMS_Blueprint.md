# FGCK Mbagathi LCA Online Church Management System
## Full System Development Blueprint

This blueprint translates the provided scope into a complete design for an online church management platform for **FGCK Mbagathi LCA** and its seven branches:

- Kandisi
- Mbagathi
- Olekasasi
- Tuala
- Rangau
- Baraka
- Rimpa

The baseline requirement is centralized LCA oversight with branch-level autonomy for day-to-day operations.

---

## 1) System Name

**Primary:** FGCK Mbagathi LCA Church Management System  
**Suggested short name:** FGCK Mbagathi CMS

Alternative names:
- FGCK Connect
- Mbagathi LCA Digital Office
- FGCK ChurchHub
- FGCK Mbagathi e-Church System

## 2) System Purpose

A secure web-based platform to manage church administrative, spiritual, financial, membership, pastoral, and operational functions.

### Administration Levels
- **LCA Level:** Central oversight across all branches.
- **Branch Level:** Branch-specific management and execution.

### Outcome
Leaders can access real-time information on:
- Membership
- Attendance
- Giving/Finance
- Ministries
- Events
- Welfare
- Projects
- Assets
- Pastoral care
- Reports

## 3) Core Branch Structure

| Level | Unit |
|---|---|
| LCA | FGCK Mbagathi LCA |
| Branch 1 | Kandisi Branch |
| Branch 2 | Mbagathi Branch |
| Branch 3 | Olekasasi Branch |
| Branch 4 | Tuala Branch |
| Branch 5 | Rangau Branch |
| Branch 6 | Baraka Branch |
| Branch 7 | Rimpa Branch |

Each branch maintains its own users, members, services, finances, ministries, assets, and reports while LCA retains consolidated visibility.

## 4) System Architecture

### 4.1 Recommended Architecture
A **multi-branch web application** with strict **role-based access control (RBAC)** and branch-scoped permissions.

## 5) Recommended Technology Stack

| Layer | Recommended Technology |
|---|---|
| Frontend | React + TypeScript + Tailwind CSS |
| Backend | Node.js + Express + TypeScript |
| Database | PostgreSQL |
| ORM | Prisma |
| Authentication | JWT with refresh tokens |
| File Storage | Local server storage initially; cloud storage later |
| Reports | PDFKit / Puppeteer (PDF), ExcelJS (Excel) |
| SMS | Africa’s Talking or local SMS gateway |
| Payments | M-Pesa Daraja API |
| Hosting | VPS, cloud server, or cPanel-compatible deployment |
| Backups | Automated daily database backups |
| Security | HTTPS, RBAC, audit logs, hashed passwords |

## 6) Main System Modules

### 6.1 Dashboard Module

#### LCA Dashboard
- Total members across all branches
- Branch-wise member breakdown
- Latest Sunday attendance by branch
- Consolidated monthly giving
- Upcoming LCA/branch events
- Pending approvals (finance/welfare/requisitions/reports)
- Active projects
- Welfare and pastoral care open cases
- Inactive members
- Submitted/pending branch reports

#### Branch Dashboard
- Branch membership totals and trends
- Attendance trend
- Giving summary
- Upcoming services/events
- Ministry activity
- Pending tasks/reports
- Welfare and visitor follow-up
- Project progress

### 6.2 Branch Management Module

Branch fields include branch ID, code, location, GPS (optional), leaders, contacts, service times, status, and metadata.

Core features:
- Add/edit/deactivate branch
- Assign branch leaders
- View branch members, finance, attendance
- Generate branch reports
- Cross-branch comparisons

### 6.3 Member Management Module

Supports categories such as full members, visitors, youth, children, elders, workers, ministry leaders, widows/widowers, and married couples.

Core features:
- Add/edit/search/filter members
- Import/export (Excel)
- Member card generation
- Attendance and giving tracking
- Household/ministry linking
- Follow-up assignments

### 6.4 Household & Family Module

Features:
- Create households
- Link spouses/children/dependants
- Track household attendance, pastoral visits, welfare needs
- Family messaging, milestones, inactive-family detection

### 6.5 Attendance Management Module

Attendance types include Sunday, midweek, prayer, youth, women/men fellowships, Sunday school, choir, evangelism, and conferences.

Capture options:
- Manual entry
- Member check-in
- Visitor entry
- Bulk upload (Excel)
- QR code (Phase 2)

Reports:
- Branch/service/weekly/monthly attendance
- Absentee reports
- Visitor follow-up
- Ministry and age-group attendance

### 6.6 Finance & Giving Module

Includes income and expense category management, strict permissions, audit logging, and approval workflows.

Controls:
- Branch treasurers see branch data only
- LCA treasurer sees consolidated data
- Auditors are read-only
- Soft delete for transactions
- Logged edits for accountability

### 6.7 M-Pesa Integration Module

- **Phase 1:** Manual M-Pesa transaction capture
- **Phase 2:** Daraja API integration (STK push, reconciliation, auto-import, confirmations)

### 6.8 Ministry & Department Module

Manage ministries, leaders, schedules, budgets, activities, attendance, and ministry reporting.

### 6.9 Events & Church Calendar Module

Central calendar supporting service and event planning with budget, attendance, status tracking, reminders, and calendar export.

### 6.10 Communication Module

Channels:
- SMS
- Email
- WhatsApp-ready message format
- In-system announcements

Targeting by branch, ministry, age, gender, status, leadership role, and follow-up groups.

### 6.11 Pastoral Care Module

Case handling for new believers, visitors, sick members, bereavement, counseling, prayer, discipleship, etc.

Confidential access limited to:
- LCA overseer
- Branch pastor
- Assigned pastoral care officers
- Authorized pastoral users

### 6.12 Welfare & Support Module

Request and disbursement workflow for welfare categories (medical, emergency, school fees, bereavement, food, etc.) with approvals and follow-up notes.

### 6.13 Document Management Module

Stores minutes, reports, budgets, financial statements, forms, sacramental records, policy docs, letters, and photos.

### 6.14 Asset & Inventory Module

Tracks church assets by branch including value, condition, custodian, status, and maintenance history.

### 6.15 Projects & Development Module

Tracks project budget, fundraising progress, milestones, expenses, risks, and updates.

## 7) User Roles & Permissions

### 7.1 Core Roles
- Super Admin
- LCA Overseer/Admin
- Branch Pastor
- Assistant Pastor
- Church/Branch Secretary
- Treasurer / Finance Officer
- Ministry Leader
- Attendance Officer
- Pastoral Care Officer
- Welfare Officer
- Member
- Viewer/Auditor

### 7.2 Permission Model
Enforce module-level and branch-level RBAC with least privilege, including confidential segmentation for finance and pastoral notes.

## 8) Key Workflows
- Member registration
- Finance collection
- Expense approval
- Visitor follow-up

## 9) Database Design

### 9.1 Core Tables (by domain)
- **Administration:** users, roles, permissions, user_roles, branches, audit_logs
- **Membership:** members, households, household_members, visitors, member_status_history
- **Attendance:** services, attendance_sessions, attendance_records, visitor_attendance
- **Finance:** transactions, giving_categories, expense_categories, budgets, budget_items, pledges, requisitions, approvals
- **Ministries:** ministries, ministry_members, ministry_activities, ministry_reports
- **Events:** events, event_attendance, event_reports
- **Pastoral/Welfare:** pastoral_cases, pastoral_notes, welfare_requests, welfare_disbursements
- **Assets/Documents/Projects:** documents, assets, asset_maintenance, projects, project_milestones, project_contributions

## 10) Suggested API Structure

### 10.1 Authentication
- POST `/api/auth/login`
- POST `/api/auth/logout`
- POST `/api/auth/refresh`
- POST `/api/auth/change-password`

### 10.2 Branches
- GET `/api/branches`
- POST `/api/branches`
- GET `/api/branches/:id`
- PUT `/api/branches/:id`
- DELETE `/api/branches/:id` (deactivate)

### 10.3 Members
- GET `/api/members`
- POST `/api/members`
- GET `/api/members/:id`
- PUT `/api/members/:id`
- POST `/api/members/import`
- GET `/api/members/export`

### 10.4 Finance
- GET `/api/transactions`
- POST `/api/transactions`
- PUT `/api/transactions/:id`
- POST `/api/requisitions`
- POST `/api/requisitions/:id/approve`
- GET `/api/reports/finance/monthly`

### 10.5 Attendance
- POST `/api/attendance/session`
- POST `/api/attendance/record`
- GET `/api/attendance/reports`

### 10.6 Reports
- GET `/api/reports/dashboard`
- GET `/api/reports/members`
- GET `/api/reports/attendance`
- GET `/api/reports/finance`
- GET `/api/reports/export/pdf`
- GET `/api/reports/export/excel`

## 11) User Interface Layout

### 11.1 Main Navigation
Dashboard, Branches, Members, Families, Attendance, Finance, Ministries, Events, Communication, Pastoral Care, Welfare, Projects, Assets, Documents, Reports, Users & Roles, Settings.

### 11.2 Dashboard Cards (example)
- Total Members
- Sunday Attendance
- Monthly Giving
- Visitors This Month
- Active Welfare Cases
- Upcoming Events
- Pending Reports
- Active Projects

## 12) MVP Scope

### Include in MVP (Release 1)
- Authentication and RBAC
- Branch management
- Member management
- Attendance tracking
- Finance/giving
- Events/calendar
- Basic communication
- Dashboard/reporting
- Basic pastoral care and welfare
- Basic document upload

### Phase 2+
- Assets
- Projects
- M-Pesa API integration
- QR attendance

## 13) Development Phases

- **Phase 1 (8–12 weeks):** MVP foundation
- **Phase 2 (6–8 weeks):** pastoral/welfare/ministry/docs/projects/assets
- **Phase 3 (6–8 weeks):** SMS/email/M-Pesa integration, exports, reminders, advanced audit
- **Phase 4 (4–6 weeks):** mobile optimization, self-service portal, tuning, backup automation

## 14) Security & Data Protection

### Security Requirements
- HTTPS
- Password hashing
- RBAC and branch scoping
- Audit trails
- Secure session management
- Backup automation
- Login attempt controls
- Sensitive-field protections

### Sensitive Data (restricted)
- Giving records
- Pastoral notes
- Welfare/counseling records
- ID/phone/family details

## 15) Required Reports

- Membership reports
- Attendance reports
- Finance reports
- Operations reports (branch/ministry/event/pastoral/welfare/assets/projects/documents/audit)

## 16) System Settings

Configurable settings include church profile, branches, service types, categories, ministries, roles/permissions, communication templates, fiscal year, currency, and backup options.

## 17) Deployment Plan

### Recommended Hosting
**VPS with daily automated backups** for best cost-control and flexibility.

### Deployment Components
- Domain
- SSL
- API server
- Frontend app
- PostgreSQL
- File storage + backup storage
- Email/SMS setup
- Initial admin provisioning

## 18) Maintenance Plan

- Daily backups
- Monthly security updates
- Quarterly access reviews
- Monthly report/data/finance verification
- User support and periodic training

## 19) Training Plan

Role-based training for LCA leaders, pastors, secretaries, treasurers, ministry leaders, welfare team, and members.

## 20) Final Developer Instruction

Build a secure, scalable, multi-branch platform that digitizes the full church operations lifecycle.

- **Release 1 (MVP):** login, branches, members, attendance, finance, events, communication, dashboards, reports.
- **Release 2:** pastoral care, welfare, assets, projects, documents, integrations.

This creates a practical transition path from manual administration to full digital church operations for FGCK Mbagathi LCA.
