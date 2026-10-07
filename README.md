<div align="center">

# 🏫 CampusDesk

### Multi-Institute School Management Platform

**Student records, fees, teachers, classes, documents and promotions — one secure desk for every campus.**

[![React](https://img.shields.io/badge/React-19-61DAFB?style=for-the-badge&logo=react&logoColor=black)](https://react.dev/)
[![Vite](https://img.shields.io/badge/Vite-6-646CFF?style=for-the-badge&logo=vite&logoColor=white)](https://vite.dev/)
[![Supabase](https://img.shields.io/badge/Supabase-PostgreSQL-3ECF8E?style=for-the-badge&logo=supabase&logoColor=white)](https://supabase.com/)
[![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-06B6D4?style=for-the-badge&logo=tailwindcss&logoColor=white)](https://tailwindcss.com/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?style=for-the-badge&logo=typescript&logoColor=white)](https://www.typescriptlang.org/)

</div>

---

## 📖 Overview

**CampusDesk** is a production-style, multi-tenant school management system built for real institutes — not a classroom demo. A **Super Admin** onboards and approves schools; each **School Admin** then runs their own campus end-to-end: students, teachers, classes, subjects, marks, fee collection, documents and session promotions — all isolated per institute through strict PostgreSQL Row-Level Security.

The backend runs on **Supabase (PostgreSQL + Auth + Storage)** with a fully documented relational schema, and an optional **Express/pg service layer** for direct database operations, migrations and data repair scripts.

---

## ✨ Features

- **🏢 Multi-institute tenancy** — schools register, get approved/suspended by a Super Admin, and operate in fully isolated data scopes
- **👥 Three-role access control** — Super Admin, School Admin, Teacher — enforced by RLS policies, not just UI hiding
- **🎓 Complete student lifecycle** — admissions, class/section assignment, status tracking (active, suspended, graduated, transferred)
- **💰 Fee management** — monthly fee structures, payments, dues tracking and fee updates per student
- **👩‍🏫 Teacher management** — profiles, subject assignments, document records and class responsibilities
- **📊 Marks monitoring** — class/subject marks entry with monitoring views for admins
- **📁 Teacher documents vault** — secure document upload and management backed by Supabase Storage
- **🔄 Session promotions** — one-click student promotions to the next class/session with repair tooling
- **🔐 Hardened auth** — Supabase Auth with password-recovery flows, schema-cache repair scripts and audit-safe delete policies
- **🤖 AI-assisted tooling** — Gemini-powered document generation helpers for administrative paperwork

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Frontend | React 19, Vite 6, TypeScript 5.8 |
| Styling | Tailwind CSS 4, clsx, tailwind-merge |
| Routing & State | React Router 7, SWR 2, Context API |
| Backend | Supabase (PostgreSQL, Auth, Storage), Express 4 + `pg` service layer |
| AI | Google Gemini (`@google/genai`) |
| Data utils | Papaparse, xlsx, date-fns, Recharts |
| UX | Lucide icons, Motion animations, react-hot-toast, react-easy-crop |
| Deployment | Netlify (`netlify.toml`) |

---

## 🏗️ Architecture

```
Browser (React SPA)
    │  Supabase JS client
    ▼
Supabase ──► PostgreSQL (RLS per school) ──► Auth ──► Storage (documents, logos)
    ▲
    │  Direct SQL / service scripts (Node + pg)
    │
Express/pg utilities ── migrations, fixes, audits, CSV imports
```

- **Data model** — documented in `CampusDesk_Backend_Documentation.md`: schools, profiles, academic sessions, classes, sections, teachers, students, fees, subjects and documents, with typed enums (`school_status`, `user_role`, `student_status`).
- **Security** — `secure_multi_tenant_rls.sql` plus cascade-delete and delete-policy fixes keep every query scoped to the caller's school.
- **Ops scripts** — `alter-table`, `fix-*`, `check-schema`, `reload-schema` and audit tests let an admin inspect and repair a live database safely.

---

## 🚀 Getting Started

### Prerequisites

- Node.js 20+
- A Supabase project (URL + anon key)

### Installation

```bash
git clone https://github.com/mwaleed-pk/school-management-system-.git
cd school-management-system-
npm install
```

### Environment variables

Copy the template and fill in your own values — **never commit real keys**:

```bash
cp .env.example .env
```

```env
VITE_SUPABASE_URL="https://your-project.supabase.co"
VITE_SUPABASE_ANON_KEY="your-anon-key"
VITE_SUPER_ADMIN_EMAIL="admin@yourdomain.com"
VITE_SUPER_ADMIN_PASSWORD="choose-a-strong-password"
# GEMINI_API_KEY="your-gemini-key"   # optional, AI document helpers
```

### Database setup

Apply the schema and policies in the Supabase SQL Editor, in order:

1. `src/db/schema.sql`
2. `src/db/final-policies.sql` (or `fix-policies.sql` / `fix-policies2.sql`)
3. `secure_multi_tenant_rls.sql`
4. Any `fix_*.sql` relevant to your deployment

### Run

```bash
npm run dev      # dev server on http://localhost:3000
npm run build    # production build
npm run lint     # type-check (tsc --noEmit)
```

---

## 📁 Project Structure

```
├── src/
│   ├── pages/
│   │   ├── auth/            # Login, Register, ForgotPassword
│   │   ├── super-admin/     # SchoolsList, Dashboard (approvals)
│   │   └── school-admin/    # Dashboard, Students, Teachers, Classes,
│   │                        # Subjects, Fees, Marks, Documents, Promotions
│   ├── components/          # ConfirmModal, ImageCropper, Logo, WhatsAppButton, layouts
│   ├── contexts/            # AuthContext
│   ├── db/                  # schema.sql, fee/payments, policies, RLS
│   └── lib/
├── *.sql / *.js             # migration, repair and audit scripts
├── CampusDesk_Backend_Documentation.md   # full data-model reference
├── CampusDesk_Teacher_Documents_Backend.md
├── AGENTS.md
└── netlify.toml
```

---

## 🗺️ Roadmap

- [ ] Parent portal with fee receipts and progress reports
- [ ] SMS/WhatsApp fee-reminder automation
- [ ] Timetable and attendance modules
- [ ] Payroll for teachers and staff
- [ ] Multi-language UI (English / Urdu)

---

## 🤝 Contributing

Contributions are welcome. Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/your-feature`)
3. Commit with clear messages
4. Open a Pull Request describing the change

---

## 📄 License

Distributed under the **MIT License**. See `LICENSE` for details.

---

## 👤 Author

**Muhammad Waleed (MW Trader)** — [github.com/mwaleed-pk](https://github.com/mwaleed-pk)
