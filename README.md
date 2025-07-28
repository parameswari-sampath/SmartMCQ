# SmartMCQ

A simple MCQ (Multiple Choice Question) platform built with Django REST API and Next.js 15.

## 🚀 Features

- **Simple User System**: Anyone can register and login
- **Test Creation**: Teachers can create tests and add multiple-choice questions
- **Test Taking**: Students can browse and take available tests
- **Scoring**: Automatic scoring with results display
- **Privacy**: Test creators can only manage their own tests

## 🏗️ Architecture

- **Backend**: Django REST Framework with PostgreSQL
- **Frontend**: Next.js 15 with TypeScript
- **Authentication**: JWT-based authentication
- **CI/CD**: GitHub Actions for automated testing and deployment

## 📁 Project Structure

```
SmartMCQ/
├── backend/           # Django REST API
│   ├── core/         # Django project settings
│   ├── apps/         # Django applications (users, tests, etc.)
│   └── requirements.txt
├── frontend/         # Next.js application
│   ├── app/         # Next.js app directory
│   ├── components/  # Reusable components
│   └── package.json
├── .github/         # GitHub Actions workflows
└── process.yaml     # Development roadmap
```

## 🛠️ Development Setup

### Prerequisites

- Python 3.11+
- Node.js 18+
- PostgreSQL 15+

### Backend Setup

```bash
cd backend
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
python manage.py migrate
python manage.py runserver
```

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

## 🧪 Testing

### Backend Tests
```bash
cd backend
python manage.py test
```

### Frontend Tests
```bash
cd frontend
npm run test
```

### Full CI Pipeline
The project includes GitHub Actions workflows for:
- Backend CI (Django tests, linting, database checks)
- Frontend CI (Next.js build, tests, linting)
- Full-stack integration tests

## 📋 Development Process

The development follows an agile sprint-based approach. See `process.yaml` for the detailed roadmap organized into 4 sprints:

1. **Sprint 1**: Project Setup & Authentication
2. **Sprint 2**: Test Management (CRUD)
3. **Sprint 3**: Question Management
4. **Sprint 4**: Test Taking & Results

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Ensure tests pass
5. Submit a pull request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).