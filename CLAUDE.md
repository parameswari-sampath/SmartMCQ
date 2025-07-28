# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

SmartMCQ is a smart multiple-choice question platform with separate frontend and backend components.

## Repository Structure

- `frontend/` - Frontend application (likely React, Vue, or similar SPA framework)
- `backend/` - Backend API server (likely Node.js, Python, or similar)

## Development Setup

Since this project is in early development, the following commands will need to be established once the project structure is implemented:

### Frontend Development
- Navigate to `frontend/` directory for frontend-specific commands
- Common commands will likely include:
  - Install dependencies
  - Start development server
  - Build for production
  - Run tests
  - Lint code

### Backend Development  
- Navigate to `backend/` directory for backend-specific commands
- Common commands will likely include:
  - Install dependencies
  - Start development server
  - Run database migrations
  - Run tests
  - Lint code

## Architecture Notes

This project follows a separated frontend/backend architecture:
- Frontend and backend are developed and deployed independently
- API communication between frontend and backend
- Each component should have its own dependency management and build process

## Development Guidelines

- Work within the appropriate directory (`frontend/` or `backend/`) for component-specific changes
- Maintain separation of concerns between frontend and backend
- Consider API design when implementing features that span both components