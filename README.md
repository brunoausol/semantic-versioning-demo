# GitFlow, Semantic Versioning, and Conventional Commits Example

This repository demonstrates how to structure a Git project using **GitFlow**, **Semantic Versioning (SemVer)**, and **Conventional Commits**, with automated versioning powered by [GitVersion](https://gitversion.net).

---

## 🔀 GitFlow Workflow

We follow the **GitFlow branching model** to manage development, releases, and hotfixes in a structured way.  
This ensures stability in production while allowing parallel feature development.

### Branches
- **main** → Production-ready code. Every commit here is a released version.  
- **develop** → Integration branch where features and fixes are merged before release.  
- **feature/*** → Used for developing new features. Created from `develop` and merged back when complete.  
- **release/*** → Prepares a new production release. Created from `develop`, merged into both `main` and `develop`.  
- **hotfix/*** → Fixes urgent issues in production. Created from `main`, merged into both `main` and `develop`.  

### Typical Workflow
1. Create a **feature branch** from `develop`.  
2. Open a **Pull Request (PR)** into `develop` once complete.  
3. `develop` integrates new features and fixes continuously.  
4. When ready to release, create a **release branch** from `develop`, test, tag, and then merge into both `main` and `develop`.  
5. For critical production issues, create a **hotfix branch** from `main`, fix, and merge back into both `main` and `develop`.  

---

## 🔢 Semantic Versioning (SemVer)

We use [Semantic Versioning 2.0.0](https://semver.org/) to define version numbers:  


- **MAJOR** → Breaking changes (incompatible API updates).  
- **MINOR** → New features, backward-compatible.  
- **PATCH** → Backward-compatible bug fixes.  
- **PRERELEASE** → Optional, for alpha/beta/rc testing.  
- **BUILD** → Optional metadata (e.g., commit SHA).  

### Examples
- `1.4.2 → 2.0.0` → Breaking API change (**MAJOR**)  
- `1.4.2 → 1.5.0` → New feature (**MINOR**)  
- `1.4.2 → 1.4.3` → Bug fix (**PATCH**)  
- `1.4.2 → 1.5.0-alpha.1` → Alpha pre-release  
- `1.5.0-alpha.3 → 1.5.0-beta.1` → Beta release  

---

## 📝 Conventional Commits

[Conventional Commits](https://www.conventionalcommits.org/) define a consistent commit message format that maps directly to SemVer rules.

### Commit Format
```
<type>(<scope>): <description>
````
- `scope` is optional (e.g., module, service, UI).  
- Use `!` after the type to indicate a breaking change.  

### Common Commit Types

| Type     | Description                                                        | Example                                       |
|----------|--------------------------------------------------------------------|-----------------------------------------------|
| **feat** | Introduces a new feature                                           | `feat: add user authentication module`        |
| **fix**  | Bug fix                                                            | `fix(auth): correct null reference`           |
| **docs** | Documentation only                                                 | `docs: update API usage in README`            |
| **style**| Code style changes (formatting, no logic impact)                   | `style: format code with Prettier`            |
| **refactor** | Code restructuring without changing behavior                  | `refactor: simplify user service logic`       |
| **perf** | Performance improvements                                           | `perf: reduce API response time by caching`   |
| **test** | Adding or modifying tests                                          | `test: add unit tests for login service`      |
| **build**| Build system or external dependencies                              | `build: update Node.js version to 18`         |
| **ci**   | CI/CD configuration changes                                        | `ci: add GitHub Actions workflow for tests`   |
| **chore**| Maintenance tasks (not src or tests)                               | `chore: update dependencies`                  |
| **revert**| Revert a previous commit                                          | `revert: revert feat: add user authentication module` |

### Impact on Versioning
- **feat** → MINOR version bump.  
- **fix**, **chore**, **docs**, etc. → PATCH version bump.  
- **BREAKING CHANGE (!)** → MAJOR version bump.  

#### Examples
- `fix(auth): correct null reference in login` → `1.4.2 → 1.4.3` (**PATCH**)  
- `feat(api): add new endpoint for user profile` → `1.4.2 → 1.5.0` (**MINOR**)  
- `feat!: remove deprecated authentication flow` → `1.4.2 → 2.0.0` (**MAJOR**)  
- `feat(ui): implement new dashboard (on develop branch)` → Pre-release `1.6.0-alpha.1` 

