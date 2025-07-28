# Git Branching Strategy for SmartMCQ

## 🌳 Branch Structure Overview

Our project follows **Git Flow** branching model with five main branch types:

```
production (stable, production-ready code)
    ↑
staging (pre-production testing)
    ↑
develop (integration branch for features)
    ↑
feature/sprint-1-auth (individual features)
feature/sprint-2-tests
feature/sprint-3-questions
    ↑
test/feature-name (dedicated testing branches)
```

## 🎯 Why Use Branching Strategy?

### **Benefits:**
1. **Parallel Development**: Multiple developers can work on different features simultaneously
2. **Code Stability**: Production branch always contains stable, tested code
3. **Feature Isolation**: Each feature is developed in isolation, preventing conflicts
4. **Easy Rollbacks**: Can quickly revert problematic features without affecting others
5. **CI/CD Integration**: Different automated testing/deployment for each branch type
6. **Code Review Process**: All changes go through pull requests before merging

### **Real-world Example:**
- Developer A works on `feature/user-authentication`
- Developer B works on `feature/test-creation`
- Both merge to `develop` → tested → then merge to `production`
- If auth has bugs, only that feature is reverted, test-creation remains unaffected

## 📋 Branch Types & Purposes

### 1. **Production Branch** (`production`)
- **Purpose**: Contains only stable, production-ready code
- **Protected**: No direct commits allowed
- **Deployment**: Auto-deploys to production server
- **Testing**: Full regression testing before deployment

### 2. **Staging Branch** (`staging`)
- **Purpose**: Pre-production testing environment
- **Base for**: Final testing before production release
- **Testing**: User acceptance testing, performance testing, security testing
- **Deployment**: Auto-deploys to staging server (mirrors production)
- **Data**: Uses production-like data for realistic testing

### 3. **Develop Branch** (`develop`)
- **Purpose**: Integration branch where features are combined and tested
- **Base for**: All new feature branches
- **Testing**: Automated CI/CD pipeline runs full test suite
- **Deployment**: Auto-deploys to development environment

### 4. **Feature Branches** (`feature/sprint-X-feature-name`)
- **Purpose**: Individual feature development
- **Naming**: `feature/sprint-1-authentication`, `feature/sprint-2-test-crud`
- **Lifespan**: Created from `develop`, merged back to `develop`
- **Testing**: Basic unit tests and feature-specific tests

### 5. **Test Branches** (`test/feature-name` or `test/integration`)
- **Purpose**: Dedicated testing of specific features or integrations
- **Use Cases**: 
  - Complex feature testing that needs isolation
  - Integration testing across multiple features
  - Performance testing with specific configurations
  - Bug reproduction and fixing
- **Lifespan**: Temporary, deleted after testing is complete

## 🔄 Workflow Process

### Starting a New Feature:
```bash
# 1. Switch to develop and pull latest changes
git checkout develop
git pull origin develop

# 2. Create new feature branch
git checkout -b feature/sprint-1-auth

# 3. Work on your feature (make commits)
git add .
git commit -m "Add user registration API"

# 4. Push feature branch
git push -u origin feature/sprint-1-auth

# 5. Create Pull Request: feature/sprint-1-auth → develop
```

### Code Review & Merge Process:
```bash
# After PR is approved and merged to develop:
# 1. Delete local feature branch
git branch -d feature/sprint-1-auth

# 2. Switch back to develop
git checkout develop
git pull origin develop

# 3. Ready for next feature!
```

### Release Process:
```bash
# When develop is stable and ready for production:
# 1. Merge develop → staging
git checkout staging
git pull origin staging
git merge develop
git push origin staging

# 2. Test thoroughly on staging environment
# 3. After staging tests pass, merge staging → production
git checkout production
git pull origin production
git merge staging
git push origin production
```

### Creating Test Branches:
```bash
# For complex feature testing:
git checkout develop
git checkout -b test/sprint-1-auth-integration
# Run extensive tests, document results
# Delete branch after testing: git branch -d test/sprint-1-auth-integration

# For bug reproduction:
git checkout production  # or staging
git checkout -b test/bug-login-redirect
# Reproduce bug, create fix, test
```

## 📊 Branch Responsibilities by Sprint

### **Sprint 1**: Authentication & Setup
- `feature/sprint-1-backend-setup` (Django + models + database)
- `feature/sprint-1-auth-apis` (register, login, logout, user info)
- `feature/sprint-1-auth-ui` (registration & login pages)

### **Sprint 2**: Test Management  
- `feature/sprint-2-test-backend` (test model + all test APIs)
- `feature/sprint-2-test-ui` (create, edit, delete, browse tests)

### **Sprint 3**: Question Management
- `feature/sprint-3-question-backend` (question model + all question APIs) 
- `feature/sprint-3-question-ui` (add, edit, delete, view questions)

### **Sprint 4**: Test Taking & Results
- `feature/sprint-4-submission-backend` (submit test + results APIs)
- `feature/sprint-4-taking-ui` (test interface + results display)

## 🔧 API-Level Sub-branches (When Needed)

For **complex APIs** or **debugging**, create temporary sub-branches:

### **During Development:**
```bash
# Main feature branch
feature/sprint-1-auth-apis
├── api/auth-register     # Temporary sub-branch for complex register API
├── api/auth-login        # Temporary sub-branch for login API
└── api/auth-logout       # Merge these back to main feature branch
```

### **For Debugging:**
```bash
# When production issue occurs
bugfix/api-login-timeout
├── debug/login-db-query      # Isolate database issue
├── debug/login-validation    # Isolate validation issue  
└── debug/login-session       # Isolate session issue
```

### **Best Practice for API Sub-branches:**
```bash
# 1. Create main feature branch
git checkout develop
git checkout -b feature/sprint-1-auth-apis

# 2. For complex API, create sub-branch
git checkout -b api/auth-register

# 3. Work on specific API
git commit -m "feat: add user registration validation"
git commit -m "feat: add registration API endpoint"

# 4. Merge back to feature branch (squash commits)
git checkout feature/sprint-1-auth-apis  
git merge --squash api/auth-register
git commit -m "feat: complete user registration API"

# 5. Delete sub-branch
git branch -d api/auth-register

# 6. Continue with next API or merge feature to develop
```

## 🎯 Recommendation for SmartMCQ

**Use the hybrid approach:**
- **Feature-level branches** for main development (cleaner, manageable)
- **API-level sub-branches** only when:
  - API is particularly complex (>3 days work)
  - Multiple developers working on same feature
  - Debugging production issues
  - Need to isolate specific functionality

This gives you **debugging precision** when needed without **branch explosion**.

## 🚦 Branch Protection Rules

### **Production Branch**:
- ✅ Require pull request reviews (minimum 2 reviewers)
- ✅ Require status checks to pass (all CI/CD tests)
- ✅ Require up-to-date branches before merging
- ✅ Include administrators in restrictions
- ✅ Allow force pushes: NO
- ✅ Require conversation resolution before merging

### **Staging Branch**:
- ✅ Require pull request reviews (minimum 1 reviewer)
- ✅ Require status checks to pass (all CI/CD tests)
- ✅ Require up-to-date branches before merging
- ✅ Allow force pushes: NO

### **Develop Branch**:
- ✅ Require pull request reviews (minimum 1 reviewer)
- ✅ Require status checks to pass
- ✅ Require up-to-date branches before merging
- ✅ Allow force pushes: NO

### **Test Branches**:
- ❌ No protection rules (temporary branches for testing)

## 🤖 Automated Workflows

### **Feature Branches**:
- Run unit tests
- Code linting
- Basic integration tests
- Security vulnerability scanning

### **Test Branches**:
- Extended test suite
- Performance benchmarks
- Load testing
- Integration testing

### **Develop Branch**:
- Full test suite
- Integration tests
- Deploy to development environment
- Code coverage reports

### **Staging Branch**:
- Full regression testing
- User acceptance testing
- Performance testing
- Security scans
- Deploy to staging environment

### **Production Branch**:
- Final security scans
- Deploy to production
- Monitoring alerts
- Rollback procedures ready

## 🎯 Best Practices

### **Commit Messages**:
```bash
# Good examples:
git commit -m "feat: add user registration API endpoint"
git commit -m "fix: resolve login validation bug"
git commit -m "docs: update API documentation"
git commit -m "test: add unit tests for auth service"
```

### **Branch Naming**:
```bash
# Feature branches:
feature/sprint-1-user-auth
feature/sprint-2-test-crud
feature/add-email-validation

# Bugfix branches:
bugfix/fix-login-redirect
bugfix/resolve-test-scoring-error

# Hotfix branches (for production):
hotfix/security-patch-auth
```

### **Pull Request Guidelines**:
1. **Title**: Clear, descriptive summary
2. **Description**: What changed and why
3. **Testing**: How the feature was tested
4. **Screenshots**: For UI changes
5. **Checklist**: Ensure all requirements met

## 🔧 Commands Cheat Sheet

```bash
# Branch Management
git branch                          # List local branches
git branch -r                       # List remote branches
git branch -a                       # List all branches
git checkout -b feature/new-feature # Create and switch to new branch
git branch -d feature/old-feature   # Delete local branch
git push origin --delete branch-name # Delete remote branch

# Staying Updated
git fetch origin                    # Fetch all remote changes
git pull origin develop            # Pull latest develop changes
git rebase develop                  # Rebase current branch on develop

# Merging
git checkout develop               # Switch to develop
git merge feature/sprint-1-auth   # Merge feature to develop
git push origin develop           # Push merged changes
```

## 🚨 Emergency Procedures

### **Hotfix for Production**:
```bash
# 1. Create hotfix branch from production
git checkout production
git pull origin production
git checkout -b hotfix/critical-security-fix

# 2. Make fix and test thoroughly
git commit -m "hotfix: resolve critical security vulnerability"

# 3. Create PR directly to production
# 4. After merge, also merge hotfix to develop
git checkout develop
git merge hotfix/critical-security-fix
```

### **Rollback Production**:
```bash
# If production deployment fails:
# 1. Identify last working commit
git log --oneline production

# 2. Create rollback branch
git checkout production
git revert <problematic-commit-hash>
git push origin production
```

This branching strategy ensures clean, manageable development with proper testing and deployment processes.