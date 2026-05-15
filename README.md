# TaskFlow — Project Management Application

![Status](https://img.shields.io/badge/status-in%20development-yellow)
![Version](https://img.shields.io/badge/version-1.0.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)

> A lightweight task and project management web application inspired by Jira and Trello. Allows teams to organize work using boards, sprints, and task tracking.

---

## 📋 Table of Contents

- [About the Project](#about-the-project)
- [Features](#features)
- [Technologies](#technologies)
- [Architecture](#architecture)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Testing](#testing)
- [CI/CD](#cicd)
- [Team](#team)

---

## 📌 About the Project

**TaskFlow** is a project management system that helps development teams plan, track, and deliver software projects. The application supports Agile/Scrum methodology with sprints, backlogs, and Kanban boards.

**Key goal:** Provide a simple and intuitive tool for managing tasks, without the complexity of enterprise solutions.

---

## ✨ Features

- 🔐 **User Authentication** — Registration, login, roles (Admin, Manager, Developer)
- 📋 **Kanban Board** — Visual task management with drag-and-drop
- 🏃 **Sprint Management** — Create and manage sprints, track progress
- 📝 **Backlog** — Full product backlog with filtering and sorting
- 👥 **Team Management** — Invite team members, assign tasks
- 📊 **Dashboard** — Analytics, burndown chart, sprint velocity
- 🔔 **Notifications** — Real-time updates on task changes
- 🏷️ **Labels & Priorities** — Tag tasks by type and priority level

---

## 🛠️ Technologies

### Frontend
| Technology | Version | Purpose |
|---|---|---|
| React | 18.x | UI Framework |
| TypeScript | 5.x | Type safety |
| Tailwind CSS | 3.x | Styling |
| React DnD | 16.x | Drag and drop |

### Backend
| Technology | Version | Purpose |
|---|---|---|
| Node.js | 20.x | Runtime |
| Express.js | 4.x | REST API |
| PostgreSQL | 15.x | Database |
| Redis | 7.x | Caching & sessions |
| JWT | — | Authentication |

### DevOps & Tools
| Tool | Purpose |
|---|---|
| Docker | Containerization |
| GitHub Actions | CI/CD pipeline |
| Jira | Project management |
| Swagger | API documentation |

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────┐
│                   CLIENT                        │
│              React + TypeScript                 │
└────────────────────┬────────────────────────────┘
                     │ HTTP / REST API
┌────────────────────▼────────────────────────────┐
│                  SERVER                         │
│              Node.js + Express                  │
│  ┌──────────┐  ┌──────────┐  ┌──────────────┐  │
│  │  Auth    │  │ Projects │  │    Tasks     │  │
│  │  Module  │  │  Module  │  │    Module    │  │
│  └──────────┘  └──────────┘  └──────────────┘  │
└──────────┬──────────────────────────────────────┘
           │
┌──────────▼──────────────┐  ┌──────────────────┐
│      PostgreSQL          │  │      Redis        │
│   (Main Database)        │  │   (Cache/Sessions)│
└─────────────────────────┘  └──────────────────┘
```

**Methodology:** Agile / Scrum  
**Sprint duration:** 2 weeks  
**Number of sprints:** 3

---

## 🚀 Installation

### Prerequisites

Make sure you have the following installed:
- [Node.js](https://nodejs.org/) v20+
- [PostgreSQL](https://www.postgresql.org/) v15+
- [Redis](https://redis.io/) v7+
- [Git](https://git-scm.com/)

### Step 1 — Clone the repository

```bash
git clone https://github.com/vladyslavsoulf/taskflow-app.git
cd taskflow-app
```

### Step 2 — Configure environment variables

```bash
cp .env.example .env
```

Edit the `.env` file:

```env
# Server
PORT=3000
NODE_ENV=development

# Database
DB_HOST=localhost
DB_PORT=5432
DB_NAME=taskflow_db
DB_USER=postgres
DB_PASSWORD=your_password

# JWT
JWT_SECRET=your_secret_key
JWT_EXPIRES_IN=7d

# Redis
REDIS_HOST=localhost
REDIS_PORT=6379
```

### Step 3 — Install dependencies

```bash
# Backend
cd server
npm install

# Frontend
cd ../client
npm install
```

### Step 4 — Set up the database

```bash
cd server
npm run db:migrate
npm run db:seed
```

### Step 5 — Run the application

```bash
# Development mode (both frontend and backend)
npm run dev

# Or separately:
cd server && npm run dev    # Backend on port 3000
cd client && npm start      # Frontend on port 3001
```

### 🐳 Run with Docker

```bash
docker-compose up --build
```

The application will be available at: `http://localhost:3000`

---

## 📖 Usage

1. Open `http://localhost:3000` in your browser
2. Register a new account or log in with the demo credentials:
   - **Email:** `demo@taskflow.com`
   - **Password:** `Demo1234!`
3. Create a new project and invite team members
4. Add tasks to the backlog
5. Create a sprint and move tasks into it
6. Track progress on the Kanban board

---

## 📁 Project Structure

```
taskflow-app/
├── client/                  # React frontend
│   ├── src/
│   │   ├── components/      # Reusable UI components
│   │   ├── pages/           # Application pages
│   │   ├── hooks/           # Custom React hooks
│   │   ├── store/           # State management
│   │   ├── api/             # API calls
│   │   └── types/           # TypeScript types
│   └── public/
│
├── server/                  # Node.js backend
│   ├── src/
│   │   ├── controllers/     # Request handlers
│   │   ├── models/          # Database models
│   │   ├── routes/          # API routes
│   │   ├── middleware/      # Auth, validation, etc.
│   │   ├── services/        # Business logic
│   │   └── utils/           # Helper functions
│   ├── migrations/          # Database migrations
│   └── tests/               # Tests
│
├── .github/
│   └── workflows/           # GitHub Actions CI/CD
├── docker-compose.yml
├── .env.example
└── README.md
```

---

## 📡 API Documentation

Full API documentation is available via Swagger after starting the server:

```
http://localhost:3000/api/docs
```

### Main endpoints:

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/auth/register` | Register new user |
| POST | `/api/auth/login` | Login |
| GET | `/api/projects` | Get all projects |
| POST | `/api/projects` | Create project |
| GET | `/api/projects/:id/tasks` | Get project tasks |
| POST | `/api/tasks` | Create task |
| PUT | `/api/tasks/:id` | Update task |
| DELETE | `/api/tasks/:id` | Delete task |
| GET | `/api/sprints/:id` | Get sprint info |

---

## 🧪 Testing

```bash
# Run all tests
npm test

# Unit tests only
npm run test:unit

# Integration tests
npm run test:integration

# Test coverage report
npm run test:coverage
```

**Test strategy:**
- **Unit tests** — Individual functions and components (Jest)
- **Integration tests** — API endpoints (Supertest)
- **E2E tests** — User flows (Cypress)

---

## ⚙️ CI/CD

The project uses **GitHub Actions** for automated CI/CD.

### Pipeline stages:

```
Push to branch
     │
     ▼
┌─────────────┐
│   Lint &    │
│   Format    │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    Tests    │
│  (Jest +    │
│  Coverage)  │
└──────┬──────┘
       │
       ▼
┌─────────────┐
│    Build    │
│   Docker    │
│   Image     │
└──────┬──────┘
       │ (only on main)
       ▼
┌─────────────┐
│   Deploy    │
│ to Staging  │
└─────────────┘
```

Configuration file: `.github/workflows/ci.yml`

---

## 👤 Team

| Name | Role |
|---|---|
| Vladislav | Full-stack Developer / Project Manager |

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

*Developed as part of the "Software Development Management" course — Alecu Russo State University, Bălți*
