# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

SmartMCQ is a simple MCQ (Multiple Choice Question) platform built with **Django REST API + Next.js 15**.

### Core Features:
- **Simple User System**: Anyone can register/login (no separate teacher/student roles)
- **Test Creation**: Users can create tests and add 4-option MCQ questions
- **Test Taking**: Users can browse and take available tests
- **Privacy**: Test creators can only manage their own tests
- **Scoring**: Automatic scoring with results display only

## Tech Stack

- **Backend**: Django REST Framework + PostgreSQL
- **Frontend**: Next.js 15 + TypeScript
- **Authentication**: JWT-based
- **CI/CD**: GitHub Actions
- **Project Management**: GitHub Projects with 4 sprints

## Repository Structure

```
SmartMCQ/
├── backend/              # Django REST API
│   ├── core/            # Django settings
│   ├── apps/            # Django apps (users, tests, etc.)
│   ├── requirements.txt
│   └── manage.py
├── frontend/            # Next.js application  
│   ├── app/            # Next.js app directory
│   ├── components/     # Reusable components
│   └── package.json
├── .github/workflows/   # CI/CD pipelines
├── process.yaml        # 40-step development roadmap
├── BRANCHING_STRATEGY.md # Git workflow guide
├── DEVELOPMENT_FLOW.md  # Daily development process
└── README.md
```

## Branching Strategy

**5-Branch Git Flow:**
- `production` - Live, stable code
- `staging` - Pre-production testing  
- `develop` - Feature integration
- `feature/*` - Individual feature development
- `test/*` - Dedicated testing (when needed)

**Workflow**: `feature/sprint-X-name` → `develop` → `staging` → `production`

## Development Commands

### Backend (Django):
```bash
cd backend
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver     # Port 8000
python manage.py test
```

### Frontend (Next.js):
```bash
cd frontend  
npm install
npm run dev                    # Port 3000
npm run build
npm run test
npm run lint
```

### Git Workflow:
```bash
# Start new feature
git checkout develop && git pull origin develop
git checkout -b feature/sprint-X-feature-name

# Daily work
git add . && git commit -m "feat: description"
git push origin feature/sprint-X-feature-name

# Create PR
gh pr create --title "Title" --body "Description"
```

## Sprint-Based Development

**Current Status**: Ready to start Sprint 1

### Sprint 1: Authentication & Setup (Due: Aug 15)
**Goal**: Users can register, login, and access platform
- ✅ Django project setup
- ✅ Next.js project setup  
- ✅ User model & auth APIs
- ✅ Registration/login UI

### Sprint 2: Test Management (Due: Aug 30) 
**Goal**: CRUD operations for tests
- Test model creation
- Test CRUD APIs (create, read, update, delete)
- Teacher dashboard UI
- Student browse tests UI

### Sprint 3: Question Management (Due: Sep 15)
**Goal**: Question CRUD operations  
- Question model (4 options + correct answer)
- Question CRUD APIs
- Add/edit/delete question UI
- View questions list UI

### Sprint 4: Test Taking & Results (Due: Sep 30)
**Goal**: Complete platform functionality
- Test submission API
- Results calculation
- Test taking interface
- Results display

## GitHub Project Management

- **Repository**: https://github.com/parameswari-sampath/SmartMCQ
- **Project Board**: GitHub Projects (ID: 3)
- **Issues**: Sprint tasks with labels (sprint-1, backend, frontend)
- **Milestones**: 4 sprints with due dates

## Important Development Notes

### API-First Approach:
Each feature follows: **API Development → UI Implementation → Integration Testing**

### Process Reference:
- **Detailed roadmap**: See `process.yaml` (40 specific tasks)
- **Git workflows**: See `BRANCHING_STRATEGY.md`  
- **Daily process**: See `DEVELOPMENT_FLOW.md`

### Testing Strategy:
- **Feature branches**: Unit tests, basic integration
- **Develop branch**: Full test suite, deploy to dev environment
- **Staging branch**: Regression tests, UAT, deploy to staging
- **Production branch**: Final security scans, deploy to production

### Next Steps for New Development:
1. Check GitHub Project board for current sprint tasks
2. Create feature branch: `feature/sprint-X-task-name`
3. Follow API-first development (backend → frontend → integration)
4. Create PR to develop branch
5. After merge, deploy to staging for testing

## Quick Start for Development

```bash
# 1. Start new feature
git checkout develop && git pull origin develop
git checkout -b feature/sprint-1-auth-api

# 2. Check current sprint in process.yaml or GitHub Issues
# 3. Develop API first, then UI
# 4. Test integration
# 5. Create PR and get review
# 6. After merge, move to next task

# Current: Start with Sprint 1 tasks from GitHub Issues
```

This project is fully configured with professional development workflows, automated testing, and agile project management. All documentation and processes are ready for immediate development.