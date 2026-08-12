# Portfolio Architecture

## 1. Overview

The Chariey Portfolio is a full-stack, content-driven personal portfolio platform.

Unlike a traditional static portfolio where professional information is hardcoded directly into frontend components, this application separates **content management** from **presentation**.

The system consists of three primary layers:

1. **React frontend** — responsible for presentation and user interaction.
2. **Flask backend** — responsible for business logic and API communication.
3. **PostgreSQL database** — responsible for persistent application data.

An authenticated administration dashboard allows the portfolio owner to manage professional content without modifying frontend source code.

```text
┌─────────────────────────────────────────────────────────────┐
│                        PUBLIC USERS                          │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                     React Frontend                          │
│                   TypeScript + Tailwind                     │
│                                                             │
│  Pages │ Components │ Hooks │ Services │ State │ Routing    │
└────────────────────────────┬────────────────────────────────┘
                             │
                         HTTPS / REST
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                      Flask Backend                          │
│                                                             │
│ Routes │ Controllers │ Services │ Models │ Validation       │
│ Authentication │ Authorization │ Integrations               │
└────────────────────────────┬────────────────────────────────┘
                             │
                             ▼
┌─────────────────────────────────────────────────────────────┐
│                     PostgreSQL                              │
│                                                             │
│ Projects │ Experience │ Skills │ Testimonials │ Users       │
│ Education │ Certifications │ Messages │ Resume              │
└─────────────────────────────────────────────────────────────┘
```

---

# 2. Architectural Goals

The architecture is designed around the following principles:

* Separation of concerns
* Maintainability
* Scalability
* Security
* Reusability
* Testability
* Accessibility
* Performance
* Clear data ownership
* Minimal coupling
* Easy future modification

The system should allow professional content to change without requiring frontend code changes.

For example, adding a new project should involve creating a database record through the administration dashboard rather than modifying a React component.

---

# 3. High-Level Architecture

The application follows a **client-server architecture**.

The React application acts as the client.

The Flask application acts as the API server.

PostgreSQL acts as the persistent data store.

```text
                         ┌───────────────┐
                         │    Browser    │
                         └───────┬───────┘
                                 │
                                 ▼
                       ┌──────────────────┐
                       │  React + Vite    │
                       │   TypeScript     │
                       └────────┬─────────┘
                                │
                         HTTP / HTTPS
                                │
                                ▼
                       ┌──────────────────┐
                       │   Flask REST API │
                       └────────┬─────────┘
                                │
                         SQLAlchemy ORM
                                │
                                ▼
                       ┌──────────────────┐
                       │   PostgreSQL     │
                       └──────────────────┘
```

The frontend does **not** connect directly to PostgreSQL.

All database operations are performed by the backend.

---

# 4. Repository Structure

The repository is divided into frontend, backend, and documentation.

```text
portfolio/
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── assets/
│   │   ├── components/
│   │   ├── contexts/
│   │   ├── features/
│   │   ├── hooks/
│   │   ├── layouts/
│   │   ├── pages/
│   │   ├── routes/
│   │   ├── services/
│   │   ├── types/
│   │   ├── utils/
│   │   ├── App.tsx
│   │   └── main.tsx
│   │
│   ├── package.json
│   ├── tsconfig.json
│   ├── vite.config.ts
│   └── ...
│
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── config.py
│   │   ├── extensions.py
│   │   │
│   │   ├── models/
│   │   ├── routes/
│   │   ├── schemas/
│   │   ├── services/
│   │   ├── integrations/
│   │   └── utils/
│   │
│   ├── migrations/
│   ├── tests/
│   ├── requirements.txt
│   └── ...
│
├── docs/
│   ├── PRD.md
│   ├── ARCHITECTURE.md
│   └── API.md
│
├── .gitignore
└── README.md
```

The exact structure may evolve as the project develops, but new additions should preserve the separation of responsibilities.

---

# 5. Frontend Architecture

The frontend uses:

* React
* TypeScript
* Vite
* Tailwind CSS
* React Router
* Axios

The frontend follows a component-based architecture.

```text
React Application
│
├── Pages
│
├── Layouts
│
├── Components
│
├── Features
│
├── Hooks
│
├── Contexts
│
├── Services
│
├── Types
│
└── Utilities
```

---

# 6. Pages

The `pages` directory contains route-level components.

Examples:

```text
pages/
├── Home/
├── About/
├── Projects/
├── ProjectDetails/
├── Experience/
├── Contact/
├── Resume/
├── Login/
└── NotFound/
```

A page is responsible for composing components and presenting the content required for a particular route.

Pages should avoid containing large amounts of business logic.

---

# 7. Components

The `components` directory contains reusable UI components.

Examples:

```text
components/
├── Navbar/
├── Footer/
├── Button/
├── ProjectCard/
├── ProjectGrid/
├── SkillCard/
├── ExperienceCard/
├── TestimonialCard/
├── Modal/
└── Form/
```

Components should ideally have a single clear responsibility.

For example:

`ProjectCard` should display project information.

It should not be responsible for making database requests.

---

# 8. Layouts

Layouts provide shared page structures.

Examples:

```text
layouts/
├── PublicLayout/
└── AdminLayout/
```

The public layout may contain:

* Navbar
* Main content
* Footer

The admin layout may contain:

* Sidebar
* Dashboard navigation
* Header
* Main content

This prevents repeated layout code across pages.

---

# 9. Routing

React Router manages frontend navigation.

Public routes may include:

```text
/
 /about
 /projects
 /projects/:slug
 /experience
 /contact
 /resume
```

Administrative routes may include:

```text
/admin
/admin/projects
/admin/projects/new
/admin/projects/:id/edit
/admin/experience
/admin/skills
/admin/testimonials
/admin/messages
/admin/settings
```

Administrative routes must be protected.

A visitor should not be able to access admin pages simply by entering the URL.

---

# 10. Feature-Based Organization

Where functionality becomes complex, related files should be grouped by feature.

For example:

```text
features/
└── projects/
    ├── components/
    ├── hooks/
    ├── services/
    ├── types/
    └── utils/
```

This approach keeps complex functionality together rather than spreading it across unrelated directories.

Feature-based organization can be introduced gradually rather than forcing every component into a feature directory.

---

# 11. API Service Layer

Frontend API communication should be centralized.

Instead of writing Axios requests directly inside components:

```text
Component
   │
   ▼
API Service
   │
   ▼
Flask API
```

Example:

```text
services/
├── api.ts
├── projectService.ts
├── experienceService.ts
├── testimonialService.ts
└── contactService.ts
```

This provides a single location for API communication.

It also makes backend URL changes easier to manage.

---

# 12. TypeScript Types

The frontend should use explicit types for API data.

Examples:

```text
types/
├── project.ts
├── experience.ts
├── skill.ts
├── testimonial.ts
├── education.ts
├── certification.ts
├── contact.ts
└── user.ts
```

For example, a project received from the API should have a defined TypeScript structure.

This prevents accidental assumptions about API data.

Avoid unnecessary use of:

```typescript
any
```

Types should represent the actual backend API contract.

---

# 13. State Management

The application should avoid introducing a global state-management library unless the complexity actually requires one.

Local component state should be used for local concerns.

Examples:

```text
Modal open/closed
Form input
Dropdown state
Loading state
```

Context can be used for application-wide concerns such as:

```text
Authentication
Theme
```

Server data should remain conceptually separate from UI state.

If server-state complexity grows significantly, a dedicated server-state solution can be introduced later.

---

# 14. Backend Architecture

The Flask backend follows a layered architecture.

```text
HTTP Request
     │
     ▼
Routes
     │
     ▼
Controllers / Request Handlers
     │
     ▼
Services
     │
     ▼
Models / Database
     │
     ▼
PostgreSQL
```

The response travels back through the layers.

```text
PostgreSQL
     │
     ▼
Models
     │
     ▼
Services
     │
     ▼
Controller
     │
     ▼
Route
     │
     ▼
JSON Response
```

---

# 15. Application Factory

The Flask application uses the application factory pattern.

The factory is responsible for creating and configuring the Flask application.

Conceptually:

```text
create_app()
     │
     ├── Load configuration
     ├── Initialize extensions
     ├── Register blueprints/routes
     ├── Configure error handlers
     └── Return Flask application
```

This approach improves:

* Testing
* Configuration management
* Modularity
* Avoidance of circular imports
* Multiple application configurations

---

# 16. Configuration

Configuration should be separated from application initialization.

Possible configurations include:

```text
Development
Testing
Production
```

Sensitive values should come from environment variables.

Examples:

```text
SECRET_KEY
DATABASE_URL
JWT_SECRET_KEY
MAIL_USERNAME
MAIL_PASSWORD
```

No secrets should be committed to Git.

---

# 17. Extensions

Flask extensions should be initialized separately.

Potential extensions include:

```text
SQLAlchemy
Flask-Migrate
JWT
CORS
Mail
```

The extensions module should create extension instances without tightly coupling them to the Flask application.

The application factory initializes them using the Flask application.

---

# 18. Models

Models represent persistent database entities.

Potential models:

```text
User
Profile
Project
Skill
Experience
Education
Certification
Testimonial
TestimonialRequest
ContactMessage
Resume
SocialLink
```

Models should primarily represent data and database relationships.

Complex business logic should generally live in services rather than making models responsible for the entire application.

---

# 19. Database Relationships

Relationships should represent real domain relationships.

For example:

```text
Project
   │
   ├── ProjectTechnology
   │
   └── ProjectImage
```

A project may have multiple technologies and images.

Similarly:

```text
Experience
   │
   └── ExperienceTechnology
```

The exact relationships should be finalized when implementing the database schema.

---

# 20. Database Migrations

Database schema changes must be handled through migrations.

The workflow should be:

```text
Modify Model
     ↓
Generate Migration
     ↓
Review Migration
     ↓
Apply Migration
     ↓
Database Updated
```

Migrations should be committed to Git.

Production databases should never be manually modified when the change should be represented by a migration.

---

# 21. Services

Services contain application/business logic.

Examples:

```text
services/
├── project_service.py
├── experience_service.py
├── testimonial_service.py
├── contact_service.py
├── auth_service.py
└── resume_service.py
```

For example, testimonial approval logic should live in a service rather than directly inside the route.

Conceptually:

```text
Route
  ↓
Testimonial Service
  ↓
Validate
  ↓
Update Status
  ↓
Save
  ↓
Return Result
```

This makes the logic easier to test and reuse.

---

# 22. Routes / Blueprints

Routes define API endpoints.

Organize routes by resource.

Example:

```text
routes/
├── auth.py
├── projects.py
├── experience.py
├── skills.py
├── testimonials.py
├── contact.py
├── resume.py
└── admin.py
```

Routes should remain relatively thin.

They should:

1. Receive the request.
2. Validate/parse input.
3. Call the appropriate service.
4. Return the response.

Routes should not contain large blocks of business logic.

---

# 23. Schemas and Validation

API input and output should be validated.

Potential validation layer:

```text
schemas/
├── project.py
├── experience.py
├── testimonial.py
├── contact.py
└── auth.py
```

Validation should happen on the backend even if the frontend performs validation.

The frontend improves user experience.

The backend provides actual security and data integrity.

---

# 24. API Response Format

API responses should follow a predictable structure.

Successful response:

```json
{
  "success": true,
  "data": {}
}
```

Error response:

```json
{
  "success": false,
  "message": "Project not found"
}
```

Validation error:

```json
{
  "success": false,
  "message": "Validation failed",
  "errors": {
    "title": [
      "Title is required"
    ]
  }
}
```

Consistency makes frontend integration easier.

---

# 25. Public vs Administrative APIs

The API should distinguish between public and protected operations.

Public:

```text
GET /api/projects
GET /api/projects/<slug>
GET /api/skills
GET /api/experience
GET /api/testimonials
POST /api/contact
```

Administrative:

```text
POST /api/admin/projects
PATCH /api/admin/projects/<id>
DELETE /api/admin/projects/<id>

POST /api/admin/experience
PATCH /api/admin/experience/<id>

PATCH /api/admin/testimonials/<id>
```

Administrative endpoints require authentication and authorization.

---

# 26. Authentication Architecture

The admin dashboard uses token-based authentication.

```text
Admin
 │
 │ username/password
 ▼
POST /api/auth/login
 │
 ▼
Flask
 │
 ├── Find user
 ├── Verify password
 └── Generate JWT
 │
 ▼
Frontend
 │
 ▼
Authenticated API requests
```

Protected endpoints validate the token before executing administrative operations.

---

# 27. Authorization

Authentication answers:

> Who are you?

Authorization answers:

> Are you allowed to perform this action?

Both are required.

For example:

```text
Authenticated user
        │
        ▼
      ADMIN?
     /     \
   YES      NO
   │         │
   ▼         ▼
 Allow     Reject
```

The backend must enforce authorization.

Frontend route guards are useful for user experience but must never be treated as the actual security boundary.

---

# 28. Testimonial Architecture

Testimonials have a unique workflow.

```text
Administrator
      │
      ▼
Create Request
      │
      ▼
Generate Secure Token
      │
      ▼
Send Invitation
      │
      ▼
Employer
      │
      ▼
Submit Testimonial
      │
      ▼
PENDING
      │
      ▼
Administrator Review
      │
      ├───────────────┐
      ▼               ▼
   APPROVE          REJECT
      │
      ▼
 PUBLISHED
      │
      ▼
Public Portfolio
```

The invitation token should not expose internal database IDs in a predictable way.

Tokens should be cryptographically secure and have an expiration policy.

---

# 29. Content Publishing Architecture

Content should be separated into:

```text
Draft
Published
Archived
```

The backend determines which records are publicly visible.

For example:

```text
GET /api/projects
```

should return only published projects.

An administrator endpoint can retrieve drafts and archived content.

This ensures unpublished information cannot accidentally leak through the public API.

---

# 30. File Storage Architecture

Uploaded files should not be tightly coupled to the local filesystem.

The application should use a storage abstraction.

Conceptually:

```text
Application
     │
     ▼
Storage Service
     │
     ├── Local Storage
     │
     ├── Cloudinary
     │
     ├── S3
     │
     └── Supabase Storage
```

This makes future storage migration easier.

The database should store the file reference or URL rather than relying on files existing inside the Git repository.

---

# 31. Contact Message Architecture

Contact requests follow this flow:

```text
Visitor
   │
   ▼
Contact Form
   │
   ▼
Frontend Validation
   │
   ▼
POST /api/contact
   │
   ▼
Backend Validation
   │
   ▼
Contact Service
   │
   ├── Save Message
   │
   └── Send Notification
   │
   ▼
PostgreSQL
```

The system should validate and rate-limit public contact submissions to reduce abuse.

---

# 32. LinkedIn Integration Architecture

LinkedIn functionality should be isolated from the core application.

```text
backend/
└── integrations/
    └── linkedin/
```

The core application should not directly depend on LinkedIn APIs.

Instead:

```text
Portfolio Service
       │
       ▼
LinkedIn Integration
       │
       ▼
LinkedIn API
```

If LinkedIn becomes unavailable, the core portfolio must continue functioning.

The same approach can later be applied to GitHub or other external services.

---

# 33. GitHub Integration

GitHub integration can eventually provide:

* Repository information.
* Repository links.
* Languages.
* Stars.
* Project metadata.
* Recent activity.

However, GitHub API integration should be considered an enhancement rather than a dependency for the core portfolio.

Projects manually managed through the admin dashboard should continue working even if GitHub integration is unavailable.

---

# 34. Error Handling Architecture

Errors should be handled centrally where possible.

Backend responsibilities:

* Log internal errors.
* Return safe public error messages.
* Avoid exposing stack traces in production.
* Return appropriate HTTP status codes.

Frontend responsibilities:

* Display useful messages.
* Handle loading states.
* Handle empty states.
* Handle API failures.
* Avoid exposing technical errors directly to users.

---

# 35. Security Architecture

The security model follows a defense-in-depth approach.

Important boundaries include:

```text
Browser
   │
   ▼
Frontend Validation
   │
   ▼
HTTPS
   │
   ▼
Authentication
   │
   ▼
Authorization
   │
   ▼
Backend Validation
   │
   ▼
Business Logic
   │
   ▼
Database
```

The system must never trust client-side validation alone.

---

# 36. Environment Separation

The application should support:

```text
Development
Testing
Production
```

Each environment should have appropriate configuration.

Development may use:

```text
localhost
```

Production should use:

```text
HTTPS
```

Production secrets must be configured through the hosting platform.

---

# 37. Deployment Architecture

The production environment consists of:

```text
                       INTERNET
                          │
                          ▼
                 ┌─────────────────┐
                 │     Vercel      │
                 │ React Frontend  │
                 └────────┬────────┘
                          │
                         HTTPS
                          │
                          ▼
                 ┌─────────────────┐
                 │     Render      │
                 │  Flask Backend  │
                 └────────┬────────┘
                          │
                          ▼
                 ┌─────────────────┐
                 │   PostgreSQL    │
                 └─────────────────┘
```

The frontend and backend should communicate through HTTPS.

---

# 38. CI/CD Architecture

Future CI/CD can use GitHub Actions.

```text
Developer
    │
    ▼
Git Push
    │
    ▼
GitHub
    │
    ▼
GitHub Actions
    │
    ├── Lint
    ├── Test
    ├── Build
    └── Deploy
```

The pipeline should prevent broken code from being deployed when practical.

---

# 39. Testing Architecture

Testing should exist at multiple levels.

```text
Unit Tests
    │
    ▼
Service / Component Tests
    │
    ▼
API Integration Tests
    │
    ▼
End-to-End Tests
```

Not every function requires an end-to-end test.

Tests should focus on important behavior and business rules.

---

# 40. Observability

As the application grows, logging and monitoring should be introduced.

Potential areas:

* API errors.
* Authentication failures.
* Contact submissions.
* Testimonial submissions.
* Server errors.
* Performance issues.

Production logs should never contain:

* Passwords.
* JWT secrets.
* API keys.
* Private testimonial content unnecessarily.
* Sensitive personal information.

---

# 41. Scalability Strategy

The application is designed for **modest initial scale** while keeping future growth possible.

The primary scalability principles are:

### Horizontal separation

Frontend and backend are deployed independently.

### Database abstraction

SQLAlchemy separates application code from direct SQL implementation.

### Service layer

Business logic is separated from HTTP routes.

### API abstraction

The frontend communicates through APIs rather than directly accessing the database.

### Storage abstraction

File storage can be migrated without rewriting the entire application.

### Integration isolation

External services such as LinkedIn and GitHub are isolated from the core application.

---

# 42. Avoiding Overengineering

The architecture deliberately avoids introducing unnecessary complexity.

For example:

A portfolio does not initially require:

* Microservices.
* Kubernetes.
* Redis.
* Message queues.
* Event-driven architecture.
* Multiple backend services.

The application should begin as a **modular monolith**.

```text
                Modular Monolith
                       │
        ┌──────────────┼──────────────┐
        │              │              │
     Projects       Experience     Testimonials
        │              │              │
        └──────────────┼──────────────┘
                       │
                   PostgreSQL
```

If the application eventually grows enough to justify separating services, the existing modular boundaries make that migration easier.

For the current product, a well-structured Flask application is more appropriate than prematurely introducing distributed architecture.

---

# 43. Data Flow Example: Adding a Project

An administrator creates a new project.

```text
Admin
 │
 ▼
Admin Dashboard
 │
 ▼
Project Form
 │
 ▼
Project Service
 │
 ▼
POST /api/admin/projects
 │
 ▼
Flask Route
 │
 ▼
Project Service
 │
 ├── Validate
 ├── Apply business rules
 └── Create model
 │
 ▼
SQLAlchemy
 │
 ▼
PostgreSQL
 │
 ▼
Response
 │
 ▼
Admin Dashboard
```

Once published:

```text
Public Visitor
      │
      ▼
Projects Page
      │
      ▼
GET /api/projects
      │
      ▼
Flask
      │
      ▼
PostgreSQL
      │
      ▼
Published Projects
      │
      ▼
React
      │
      ▼
Project Cards
```

No React source code needs to change.

---

# 44. Data Flow Example: Employer Testimonial

```text
Administrator
      │
      ▼
Generate Testimonial Request
      │
      ▼
Secure Token
      │
      ▼
Employer receives link
      │
      ▼
Testimonial Form
      │
      ▼
POST /api/testimonials/submit/:token
      │
      ▼
Flask
      │
      ▼
Validate Token
      │
      ▼
Create Pending Testimonial
      │
      ▼
PostgreSQL
      │
      ▼
Admin Dashboard
      │
      ▼
Review
      │
      ▼
Approve
      │
      ▼
Published
      │
      ▼
Public Portfolio
```

---

# 45. Data Flow Example: Contact Message

```text
Visitor
   │
   ▼
Contact Form
   │
   ▼
POST /api/contact
   │
   ▼
Validation
   │
   ▼
Contact Service
   │
   ├── Database
   │
   └── Email Notification
   │
   ▼
Admin Dashboard
```

---

# 46. API Versioning

The initial API can use:

```text
/api/...
```

As the API evolves, versioning can be introduced:

```text
/api/v1/...
```

Versioning should be introduced when there is an actual need for backwards compatibility rather than adding complexity prematurely.

---

# 47. Documentation

The repository documentation is divided into:

```text
docs/
├── PRD.md
├── ARCHITECTURE.md
└── API.md
```

### PRD.md

Defines:

* What the product is.
* Why it exists.
* Requirements.
* Features.
* User types.
* Product goals.

### ARCHITECTURE.md

Defines:

* How the system is designed.
* Components.
* Data flow.
* Technology choices.
* Security architecture.
* Deployment architecture.

### API.md

Defines:

* API endpoints.
* Request formats.
* Response formats.
* Authentication requirements.
* Error responses.

---

# 48. Architectural Decision Records

As significant architectural decisions are made, they may be documented separately.

Future structure:

```text
docs/
└── decisions/
    ├── 001-use-flask.md
    ├── 002-use-postgresql.md
    ├── 003-use-modular-monolith.md
    └── 004-storage-abstraction.md
```

These documents should explain:

* Context.
* Decision.
* Alternatives considered.
* Consequences.

This prevents important architectural decisions from becoming tribal knowledge.

---

# 49. Definition of Architectural Success

The architecture is successful if:

* New projects can be added without frontend code changes.
* New experiences can be added without frontend code changes.
* Testimonials can be submitted securely.
* Admin functionality is protected.
* Public APIs expose only published content.
* Frontend and backend remain loosely coupled.
* Database changes are managed through migrations.
* Business logic is separated from routes.
* External integrations are isolated.
* Secrets are not committed.
* The application can be tested independently.
* The application can be deployed independently.
* Future features can be introduced without rewriting the entire system.

---

# 50. Architectural Philosophy

The architecture follows one central idea:

> **The portfolio should grow with the developer.**

The application should not need to be rebuilt every time my professional life changes.

When I gain:

* A new internship,
* A new job,
* A new project,
* A new certification,
* A new skill,
* A new achievement,
* A new testimonial,

the system should allow that information to be added through the appropriate interface.

The code defines **how the system works**.

The database defines **what professional content exists**.

The administration dashboard provides the mechanism for managing that content.

The public React application presents that content to visitors.

This separation allows the portfolio to evolve from a simple personal website into a maintainable personal professional platform without requiring unnecessary architectural complexity.
