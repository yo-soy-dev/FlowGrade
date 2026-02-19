<!--
 ███████╗██╗      ██████╗ ██╗    ██╗ ██████╗ ██████╗  █████╗ ██████╗ ███████╗
 ██╔════╝██║     ██╔═══██╗██║    ██║██╔════╝ ██╔══██╗██╔══██╗██╔══██╗██╔════╝
 █████╗  ██║     ██║   ██║██║ █╗ ██║██║  ███╗██████╔╝███████║██║  ██║█████╗
 ██╔══╝  ██║     ██║   ██║██║███╗██║██║   ██║██╔══██╗██╔══██║██║  ██║██╔══╝
 ██║     ███████╗╚██████╔╝╚███╔███╔╝╚██████╔╝██║  ██║██║  ██║██████╔╝███████╗
 ╚═╝     ╚══════╝ ╚═════╝  ╚══╝╚══╝  ╚═════╝ ╚═╝  ╚═╝╚═╝  ╚═╝╚═════╝ ╚══════╝
-->

<div align="center">

```
╔╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╗
╠╣                                                               ╠╣
╠╣   🎓  F L O W G R A D E                                      ╠╣
╠╣      ═══════════════════════════════════════════              ╠╣
╠╣      Assign. Submit. Review. Done.                            ╠╣
╠╣      Role-based assignment workflow for Mentneo.             ╠╣
╠╣                                                               ╠╣
╚╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╝
```

[![React](https://img.shields.io/badge/React_18-000000?style=for-the-badge&logo=react&logoColor=61DAFB)](https://react.dev)
[![TypeScript](https://img.shields.io/badge/TypeScript-000000?style=for-the-badge&logo=typescript&logoColor=3178C6)](https://typescriptlang.org)
[![Node.js](https://img.shields.io/badge/Node.js-000000?style=for-the-badge&logo=node.js&logoColor=339933)](https://nodejs.org)
[![MongoDB](https://img.shields.io/badge/MongoDB-000000?style=for-the-badge&logo=mongodb&logoColor=47A248)](https://mongodb.com)
[![Vite](https://img.shields.io/badge/Vite-000000?style=for-the-badge&logo=vite&logoColor=646CFF)](https://vitejs.dev)

**[What It Is](#-what-it-is) · [Workflow](#-assignment-lifecycle) · [Roles](#-roles--permissions) · [Stack](#-stack) · [Spin It Up](#-spin-it-up) · [API](#-api-reference) · [Security](#-security)**

</div>

---

## ❯ What It Is

Flowgrade is a **role-based assignment workflow platform** built for Mentneo's internal operations. Mentors create assignments, students submit multi-file work, and mentors review — all enforced by a strict three-state lifecycle with role guards at every API endpoint.

```
╔╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╗
╠╣  Mentor creates assignment  →  Status: PENDING                 ╠╣
╠╣  Student uploads files      →  Status: SUBMITTED              ╠╣
╠╣  Mentor reviews work        →  Status: REVIEWED               ╠╣
╠╣  Invalid transitions        →  400 / 403 blocked at API       ╠╣
╚╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╝
```

---

## ◈ Assignment Lifecycle

```
  ┌─────────────┐       Student        ┌─────────────┐       Mentor
  │             │      submits         │             │      reviews
  │   PENDING   │ ───────────────────▶ │  SUBMITTED  │ ──────────────▶  REVIEWED
  │             │                      │             │
  │  Created by │                      │  Files      │
  │   Mentor    │                      │  uploaded   │
  └─────────────┘                      └─────────────┘

  ❌  Pending  ──▶  Reviewed    (skip not allowed — 400 Bad Request)
  ❌  Student  creates assignment        (403 Forbidden)
  ❌  Mentor   submits assignment        (403 Forbidden)
  ❌  Student  reviews submission        (403 Forbidden)
```

---

## ◈ Roles & Permissions

```
FLOWGRADE  /  ROLES
│
├── 👨‍🏫  MENTOR
│   ├── Create assignments (title, description, deadline)
│   ├── View all student submissions
│   ├── Mark submissions as reviewed
│   ├── Track submission progress + completion rates
│   └── ❌ Cannot submit assignments
│
└── 👨‍🎓  STUDENT
    ├── View all assigned assignments
    ├── Submit multi-file work (PDF/Doc + Image + Video)
    ├── Track own submission status in real-time
    └── ❌ Cannot create or review assignments
```

| Action | Mentor | Student |
|--------|:------:|:-------:|
| Create assignment | ✅ | ❌ |
| Submit files | ❌ | ✅ |
| View all submissions | ✅ | ❌ |
| View own submissions | ❌ | ✅ |
| Mark as reviewed | ✅ | ❌ |

---

## ◈ File Uploads

```
Per Submission — max 3 files (1 of each type)
│
├── 📄  DOCUMENT     PDF · DOC · DOCX
├── 🖼️  IMAGE        JPG · JPEG · PNG · GIF
└── 🎥  VIDEO        MP4 · MOV · AVI

Limits
├── Max per file  →  10 MB (configurable via MAX_FILE_SIZE)
└── Max total     →  30 MB per submission
```

Files stored in `server/uploads/` with unique generated filenames. Metadata (path, type, size) saved in DB linked to submission ID. Extensible to AWS S3 or Cloudinary.

---

## ◈ Stack

### System Map

```
     ╔══════════════════════════════════════╗
     ║          Browser / Client            ║
     ║   React 18 + TypeScript + Vite       ║
     ║   React Router v6 + Context API      ║
     ╚══════════════╤═══════════════════════╝
                    │  Axios + JWT header
     ╔══════════════▼═══════════════════════╗
     ║          Express Server              ║
     ║          Node.js                     ║
     ║          auth.middleware.js           ║
     ║          role.middleware.js           ║
     ║          upload.js (Multer)           ║
     ╚══════╤═══════════════╤═══════════════╝
            │               │
     ┌──────┘          ┌────┘
     ▼                 ▼
╔══════════╗     ╔═══════════════╗
║ MongoDB  ║     ║  Local FS     ║
║ ───────  ║     ║  ───────────  ║
║ Users    ║     ║  uploads/     ║
║ Assigns  ║     ║  (→ S3 ready) ║
║ Submits  ║     ╚═══════════════╝
╚══════════╝
```

### At a Glance

| Layer | Technology | Role |
|-------|-----------|------|
| **Frontend** | React 18 + TypeScript | Dashboard UI, forms, routing |
| **Bundler** | Vite | Dev server + production builds |
| **HTTP** | Axios | JWT-authenticated API calls |
| **Backend** | Node.js + Express | REST API + role enforcement |
| **Database** | MongoDB + Mongoose | Users, assignments, submissions |
| **Auth** | JWT + bcrypt | Stateless auth + password hashing |
| **File Upload** | Multer | Multipart handling + validation |

---

## ◈ Spin It Up

### Prerequisites

Node.js v16+, npm or yarn, MongoDB v5+ (local or Atlas)

### Backend

```bash
# 1 — Clone
git clone <repository-url>
cd assignment-submission-system

# 2 — Install + configure
cd server
npm install
cp .env.example .env      # fill in your values

# 3 — Start
npm run dev               # → http://localhost:5000
```

### Frontend

```bash
cd client
npm install
npm run dev               # → http://localhost:5173
```

### Tests

```bash
cd server && npm test     # Backend tests
cd client && npm test     # Frontend tests
```

---

## ◈ Environment Variables

### Backend — `server/.env`

```env
# ── Server ────────────────────────────────────────────────────────
PORT=5000
NODE_ENV=development

# ── Database (choose one) ─────────────────────────────────────────
MONGODB_URI=mongodb://localhost:27017/flowgrade
# DATABASE_URL=postgresql://user:password@localhost:5432/flowgrade

# ── Auth ──────────────────────────────────────────────────────────
JWT_SECRET=your_super_secret_key                    # server-only
JWT_EXPIRE=7d

# ── File Uploads ──────────────────────────────────────────────────
MAX_FILE_SIZE=10485760                              # 10MB in bytes
UPLOAD_PATH=./uploads

# ── Cloudinary (optional — for cloud storage) ─────────────────────
CLOUDINARY_CLOUD_NAME=your_cloud_name
CLOUDINARY_API_KEY=your_api_key
CLOUDINARY_API_SECRET=your_api_secret              # server-only
```

| Variable | Required | Default |
|----------|:--------:|---------|
| `MONGODB_URI` or `DATABASE_URL` | ✅ one of | — |
| `JWT_SECRET` | ✅ | — |
| `PORT` | ❌ | 5000 |
| `JWT_EXPIRE` | ❌ | 7d |
| `MAX_FILE_SIZE` | ❌ | 10485760 |
| `UPLOAD_PATH` | ❌ | ./uploads |
| Cloudinary vars | ❌ | local storage |

### Frontend — `client/.env`

```env
VITE_API_URL=http://localhost:5000/api
```

> ⚠️ Vite requires the `VITE_` prefix for all env vars exposed to the browser.

---

## ◈ API Reference

### Auth

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| `POST` | `/api/auth/register` | Register new user | Public |
| `POST` | `/api/auth/login` | Login → returns JWT | Public |

### Assignments

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| `POST` | `/api/assignments` | Create assignment | Mentor |
| `GET` | `/api/assignments` | List all assignments | Mentor |
| `GET` | `/api/assignments/student` | Student's assignments | Student |
| `GET` | `/api/assignments/:id` | Assignment details | Mentor |

### Submissions

| Method | Endpoint | Description | Access |
|--------|----------|-------------|--------|
| `POST` | `/api/submissions/assignment/:id` | Submit files | Student |
| `GET` | `/api/submissions/my/:assignmentId` | Own submissions | Student |
| `GET` | `/api/submissions/:id` | Submission detail | Student |
| `GET` | `/api/submissions` | All submissions | Mentor |
| `PATCH` | `/api/submissions/:id/review` | Mark reviewed | Mentor |

---

## ◈ Security

| Layer | Implementation |
|-------|---------------|
| **Auth** | JWT stateless tokens |
| **Passwords** | bcrypt with salt rounds |
| **Role Guards** | `role.middleware.js` on every protected route |
| **Input Validation** | express-validator on all request bodies |
| **File Validation** | Whitelist-based type + size checking via Multer |
| **Injection Protection** | Parameterized queries + payload sanitization |
| **CORS** | Configured allowed origins |

---

## ◈ Project Structure

```
flowgrade/
│
├── server/
│   └── src/
│       ├── config/                   DB + environment config
│       ├── controllers/
│       │   ├── assignment.controller.js
│       │   ├── auth.controller.js
│       │   └── submission.controller.js
│       ├── middleware/
│       │   ├── auth.middleware.js     JWT verification
│       │   ├── role.middleware.js     Role-based access guard
│       │   └── upload.js             Multer config + validation
│       ├── models/
│       │   ├── Assignment.js
│       │   ├── Submission.js
│       │   └── User.js
│       ├── routes/
│       │   ├── assignment.route.js
│       │   ├── auth.route.js
│       │   └── submission.route.js
│       ├── scripts/
│       │   └── createAdmin.js        First admin seeder
│       └── server.js                 Entry point
│
└── client/
    └── src/
        ├── api/
        │   ├── assignment.api.ts
        │   ├── auth.api.ts
        │   ├── axios.ts              Axios instance + interceptors
        │   └── submission.api.ts
        ├── components/
        │   ├── AppLayout.tsx
        │   ├── Footer.tsx
        │   ├── Navbar.tsx
        │   ├── ProtectedRoute.tsx
        │   └── Sidebar.tsx
        ├── context/
        │   └── AuthContext.tsx       Auth state + JWT storage
        ├── pages/
        │   ├── AssignmentSubmissions.tsx
        │   ├── CreateAssignment.tsx
        │   ├── Login.tsx
        │   ├── MentorDashboard.tsx
        │   ├── Register.tsx
        │   ├── ReviewSubmission.tsx
        │   ├── StudentDashboard.tsx
        │   └── SubmitAssignment.tsx
        ├── App.tsx
        ├── main.tsx
        └── index.css
```

---

## ◈ Roadmap

```diff
+ Cloud storage (AWS S3 / Cloudinary) instead of local filesystem
+ Real-time submission updates via WebSockets
+ Email notifications on submission / approval events
+ Rich feedback — mentor comments per submission
+ Assignment templates for recurring tasks
+ Deadline reminders + overdue alerts
+ Advanced analytics dashboard (completion rates, avg review time)
+ Batch assignment operations for multiple students
+ CI/CD pipeline (GitHub Actions + Render/Vercel)
```

---

## ◈ License

```
Internal Use License

Copyright (c) 2025 Mentneo — Devansh Kumar Tiwari

All rights reserved.

This software and its source code are the exclusive property of Mentneo.
Unauthorized copying, distribution, modification, or use of this software,
in whole or in part, without prior written permission from Mentneo is
strictly prohibited.

This software is provided for internal use only and may not be shared,
sublicensed, or made publicly available in any form.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

<div align="center">

```
╔╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╦╗
╠╣   🎓  flowgrade  ·  assign. submit. review. done.             ╠╣
╚╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╩╝
```

Built with ❤️ by **Devansh Kumar Tiwari**

For support — contact the project maintainers or open an issue.

</div>
