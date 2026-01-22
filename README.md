# Project Management Tool

A full-stack application for teams to manage workspaces, projects, tasks, and collaborate in real-time.

## 🚀 Tech Stack

**Frontend:** React 19, Vite, Redux Toolkit, React Router, Tailwind CSS, Clerk Auth  
**Backend:** Node.js, Express, PostgreSQL, Prisma ORM, Inngest

## 📋 Features

- Multi-workspace management with role-based access (ADMIN/MEMBER)
- Project tracking with priority and status lifecycle
- Task management: TODO → IN_PROGRESS → DONE
- Task types: TASK, BUG, FEATURE, IMPROVEMENT, OTHER
- Real-time comments for team collaboration
- Dark mode support
- Clerk authentication & organization sync

## 🏗️ Database Schema

**Core Models:**
- User (via Clerk)
- Workspace (organization container)
- WorkspaceMember (role-based access)
- Project (belongs to workspace)
- ProjectMember (team assignment)
- Task (belongs to project, assigned to user)
- Comment (task collaboration)

## 📡 API Endpoints

```
GET/POST   /api/workspaces
GET/POST   /api/projects
GET/POST   /api/tasks
GET/POST   /api/comments
```
All endpoints require JWT authentication.

## 🚀 Quick Start

### Prerequisites
- Node.js v18+
- PostgreSQL (Neon DB recommended)
- Clerk account

### Backend Setup
```bash
cd server
npm install
# Create .env with DATABASE_URL and CLERK_SECRET_KEY
npx prisma migrate dev
npm run dev  # Runs on :5001
```

### Frontend Setup
```bash
cd client
npm install
# .env already configured
npm run dev  # Runs on :5173
```

## 📁 Project Structure

```
client/src/
├── pages/        (Layout, Dashboard, Projects, Team, Details)
├── components/   (Navbar, Sidebar, WorkspaceDropdown)
├── features/     (Redux slices: workspace, project, task, theme)
├── App.jsx       (Router setup)
└── main.jsx      (Clerk + Redux Provider)

server/
├── routes/       (workspaceRoutes, projectRoutes, taskRoutes, commentRoutes)
├── middlewares/  (authMiddleware - JWT validation)
├── inngest/      (Background jobs)
├── prisma/       (Database schema)
└── server.js     (Express + CORS setup)
```

## 🔐 Authentication Flow

1. User authenticates via Clerk
2. JWT token included in API headers
3. Backend validates with `authMiddleware`
4. Workspace membership checked before operations

## 🌐 Environment Variables

**Frontend (.env):**
```
VITE_CLERK_PUBLISHABLE_KEY
VITE_BASEURL=http://localhost:5001
```

**Backend (.env):**
```
DATABASE_URL=postgresql://...
CLERK_SECRET_KEY
PORT=5001
```

## 🎯 Redux State

```javascript
{
  workspace: { workspaces[], currentWorkspace, loading },
  project: { projects[], currentProject, loading },
  task: { tasks[], loading },
  theme: { isDark }
}
```

## 📈 Key Features

| Feature | Details |
|---------|---------|
| **Workspaces** | Switch between multiple isolated workspaces |
| **Projects** | Track with priority (LOW/MEDIUM/HIGH), status, progress |
| **Tasks** | Status workflow, type categorization, assignee tracking |
| **Comments** | Task-level collaboration |
| **Theme** | Light/dark mode with persistence |

## 🐛 Common Issues

| Issue | Fix |
|-------|-----|
| CORS Error | Verify backend CORS includes frontend URL |
| DB Connection | Use direct connection (not pooler) for migrations |
| Auth Error | Check CLERK_SECRET_KEY and PUBLISHABLE_KEY |

## 🚀 Deployment

**Frontend:** Build with `npm run build`, deploy dist/ to Vercel  
**Backend:** Deploy to Render/Railway, set environment variables

## 📝 Notes

- All API routes protected with JWT authentication
- Workspace data is isolated per organization
- Prisma handles migrations and type safety
- Inngest processes background jobs
