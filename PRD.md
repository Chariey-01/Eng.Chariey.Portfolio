# PRODUCT REQUIREMENTS DOCUMENT (PRD)

# Personal Developer Portfolio & Content Management Platform

**Project Name:** Chariey Portfolio
**Version:** 1.0
**Status:** Planned / In Development
**Owner:** Chariey
**Document Purpose:** Product requirements and implementation specification

---

# 1. Product Overview

Chariey Portfolio is a modern, full-stack personal developer portfolio designed to showcase my software engineering experience, projects, skills, education, internships, achievements, testimonials, and professional development.

Unlike a traditional static portfolio, the application will be built as a **dynamic portfolio management platform**.

The public website will display portfolio content dynamically from a Flask API and PostgreSQL database.

An authenticated administration dashboard will allow the portfolio owner to create, update, publish, unpublish, and manage portfolio content without modifying source code.

The system should be designed so that new experiences, projects, internships, testimonials, certifications, skills, and other professional information can be added through the dashboard.

---

# 2. Product Vision

The goal is to build a portfolio that evolves with my career.

The portfolio should not require a developer to modify React components or hardcode information whenever something changes.

For example:

### Current situation

I complete an internship.

I would traditionally need to:

1. Open the source code.
2. Find the experience section.
3. Hardcode the internship.
4. Modify the frontend.
5. Commit changes.
6. Deploy again.

### Desired situation

I complete an internship.

I should be able to:

1. Log into the portfolio administration dashboard.
2. Select "Experience".
3. Click "Add Experience".
4. Enter the company, role, dates, description, technologies, achievements, etc.
5. Save the experience.
6. Preview it.
7. Publish it.

The public portfolio should then automatically display the new experience.

---

# 3. Core Principle

The portfolio should be treated as a **content-driven application**, not a collection of hardcoded pages.

React should primarily be responsible for presenting data.

Flask should provide the API and application/business logic.

PostgreSQL should persist portfolio content.

The administration dashboard should manage that content.

Architecture:

```text
                    ┌─────────────────────┐
                    │       Visitor       │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │   React Frontend    │
                    │     TypeScript      │
                    │    Tailwind CSS     │
                    └──────────┬──────────┘
                               │
                            REST API
                               │
                               ▼
                    ┌─────────────────────┐
                    │    Flask Backend    │
                    │      Services       │
                    │       Routes        │
                    │       Models        │
                    └──────────┬──────────┘
                               │
                               ▼
                    ┌─────────────────────┐
                    │     PostgreSQL      │
                    └─────────────────────┘


                    ADMINISTRATOR
                          │
                          ▼
                ┌─────────────────────┐
                │   Admin Dashboard   │
                │ React + TypeScript  │
                └──────────┬──────────┘
                           │
                        REST API
                           │
                           ▼
                ┌─────────────────────┐
                │    Flask Backend    │
                └──────────┬──────────┘
                           │
                           ▼
                ┌─────────────────────┐
                │     PostgreSQL      │
                └─────────────────────┘
```

---

# 4. Technology Stack

## Frontend

* React
* TypeScript
* Vite
* Tailwind CSS
* React Router
* Axios
* React Hook Form where appropriate

## Backend

* Python
* Flask
* Flask RESTful or REST API architecture
* SQLAlchemy
* Flask-Migrate / Alembic
* PostgreSQL
* Flask-JWT-Extended
* Flask-CORS
* Werkzeug security utilities
* Flask-Mail or equivalent email service

## Deployment

Frontend:

* Vercel

Backend:

* Render

Database:

* PostgreSQL

---

# 5. User Types

The system should initially support two user roles.

## 5.1 Public Visitor

A visitor can:

* View the homepage.
* View the About section.
* View skills.
* View projects.
* View project details.
* View work experience.
* View education.
* View certifications.
* View testimonials.
* Download the CV.
* Submit a contact message.
* Access GitHub.
* Access LinkedIn.
* View publicly available professional information.

A visitor must not access the administration dashboard.

---

# 5.2 Administrator

The administrator is the portfolio owner.

The administrator can:

* Log into the dashboard.
* Manage projects.
* Manage skills.
* Manage experience.
* Manage education.
* Manage certifications.
* Manage testimonials.
* Manage profile information.
* Manage resume/CV information.
* Manage contact messages.
* Manage social links.
* Publish content.
* Unpublish content.
* Delete content.
* Edit existing content.
* Preview unpublished content.
* Manage incoming testimonials.
* Approve or reject submitted testimonials.

The initial system only requires one administrator.

The architecture should allow multiple roles in the future.

---

# 6. Authentication & Authorization

The admin dashboard must be protected.

Use:

* JWT authentication.
* Password hashing.
* Protected API endpoints.
* Role-based authorization.

Never store plaintext passwords.

The administrator should authenticate through:

```text
POST /api/auth/login
```

The backend returns an access token.

Protected requests should include the appropriate authorization header.

Example:

```text
Authorization: Bearer <token>
```

The backend must verify authentication before allowing administrative operations.

---

# 7. Public Portfolio Pages

The public frontend should contain the following sections/pages.

## Home

The homepage should contain:

* Profile introduction.
* Professional title.
* Short summary.
* Profile image.
* Primary call-to-action.
* Featured projects.
* Skills overview.
* Experience preview.
* Testimonials preview.
* Contact call-to-action.

---

# 8. About

The About section should be dynamic.

Content should come from the backend rather than being hardcoded into React.

The administrator should be able to update:

* Biography.
* Professional summary.
* Career goals.
* Interests.
* Personal introduction.
* Profile image.

---

# 9. Skills

Skills should be stored in the database.

Each skill may contain:

* Name.
* Category.
* Description.
* Proficiency level.
* Icon.
* Display order.
* Featured status.

Example categories:

```text
Frontend
Backend
Database
DevOps
Programming Languages
Tools
Other
```

The frontend should dynamically render skills.

---

# 10. Projects

Projects are a core feature of the portfolio.

Each project should support:

* Title.
* Slug.
* Short description.
* Full description.
* Problem statement.
* Solution.
* Features.
* Technologies.
* Category.
* GitHub URL.
* Live demo URL.
* Screenshots.
* Thumbnail.
* Architecture description.
* Challenges.
* Solutions.
* Lessons learned.
* Start date.
* Completion date.
* Featured status.
* Published status.
* Display order.

Initial projects include:

### CampusPulse

Full-stack campus discovery platform.

### DevCrypt

Interactive cybersecurity/CTF platform.

### Aurelia Shopping App

React-based shopping application.

### Personal Coding Tracker

Personal productivity and coding-learning tracking application.

### Wordly

Dictionary application and early shipped project.

The architecture must allow unlimited future projects.

---

# 11. Experience / Employment

The portfolio must support dynamic professional experience.

The administrator should be able to create an experience record.

Fields:

* Company.
* Job title.
* Employment type.
* Location.
* Start date.
* End date.
* Currently working.
* Description.
* Responsibilities.
* Achievements.
* Technologies.
* Company website.
* Company logo.
* Display order.
* Published status.

Employment types may include:

```text
Internship
Full-time
Part-time
Contract
Freelance
Volunteer
Apprenticeship
```

Example:

```text
Software Engineering Intern
Company XYZ
September 2026 – December 2026
```

The experience should automatically appear on the public portfolio once published.

---

# 12. Testimonials / Employer Reviews

This is a major feature.

Employers, mentors, colleagues, or supervisors should be able to submit testimonials without receiving access to the administration dashboard.

The portfolio owner should be able to generate a testimonial request link.

Example:

```text
https://portfolio.com/testimonial/<secure-token>
```

The recipient can open the link and submit:

* Name.
* Job title.
* Company.
* Email.
* Relationship to portfolio owner.
* Testimonial.
* Optional profile image.
* Optional LinkedIn URL.
* Permission to publish.

The testimonial should initially have:

```text
status = pending
```

The administrator can then:

* Approve.
* Reject.
* Edit.
* Publish.
* Unpublish.
* Delete.

Only approved and published testimonials appear publicly.

---

# 13. Testimonial Workflow

The workflow should be:

```text
Admin creates testimonial request
              ↓
Secure invitation link generated
              ↓
Employer opens link
              ↓
Employer submits testimonial
              ↓
Status = PENDING
              ↓
Admin receives notification
              ↓
Admin reviews testimonial
              ↓
      ┌───────┴────────┐
      ↓                ↓
   APPROVE           REJECT
      ↓
   PUBLISHED
      ↓
Visible on portfolio
```

The system should prevent unauthorized people from modifying testimonials.

The secure token should be difficult to guess.

---

# 14. LinkedIn Integration

The application should be designed with future LinkedIn integration in mind.

Important:

The system must NOT assume that arbitrary LinkedIn profile modifications are automatically available.

LinkedIn functionality depends on LinkedIn's available APIs, permissions, application approval, and supported use cases.

Therefore, LinkedIn integration should be implemented as an optional integration layer.

Possible future functionality:

* Connect LinkedIn account.
* Import supported professional information.
* Share published portfolio achievements.
* Share new project announcements.
* Share new experience announcements.
* Publish supported posts where the API permits it.

The architecture should isolate LinkedIn functionality inside a dedicated integration/service layer.

Example:

```text
backend/
    integrations/
        linkedin/
```

Do not tightly couple LinkedIn logic to the core portfolio models.

If LinkedIn API access is unavailable, the portfolio must work perfectly without it.

---

# 15. Resume / CV

The administrator should be able to manage the CV.

The system should support:

* Current CV.
* CV upload.
* CV replacement.
* CV download.
* CV version.
* Upload date.
* Active version.

The public user should have a:

```text
Download CV
```

button.

The backend should serve the currently active CV.

Future versions may support multiple CVs, such as:

```text
Full Stack Software Engineer CV
Backend Engineer CV
Internship CV
```

---

# 16. Contact System

Visitors should be able to contact the portfolio owner.

Contact form fields:

* Name.
* Email.
* Subject.
* Message.

The backend should validate submitted information.

Messages should be stored in the database.

The administrator should be able to view:

* Sender.
* Email.
* Subject.
* Message.
* Date.
* Read/unread status.
* Archived status.

The system may also send an email notification when a new message arrives.

---

# 17. Social Links

Social links should not be hardcoded.

The administrator should be able to manage:

* GitHub.
* LinkedIn.
* Email.
* Portfolio.
* Other professional networks.

Each social link should support:

* Platform.
* URL.
* Icon.
* Display order.
* Active status.

---

# 18. Education

Education should be dynamically managed.

Fields:

* Institution.
* Program.
* Qualification.
* Start date.
* End date.
* Description.
* Achievements.
* Institution website.
* Logo.
* Published status.

The administrator should be able to add future educational achievements without changing frontend code.

---

# 19. Certifications

The administrator should be able to add certifications.

Fields:

* Certification name.
* Issuing organization.
* Issue date.
* Expiration date.
* Credential ID.
* Credential URL.
* Certificate image/PDF.
* Description.
* Published status.

---

# 20. Admin Dashboard

The dashboard is the main content management system.

The dashboard should contain sections such as:

```text
Dashboard
│
├── Overview
├── Profile
├── Projects
├── Experience
├── Skills
├── Education
├── Certifications
├── Testimonials
├── Resume
├── Contact Messages
├── Social Links
├── Integrations
└── Settings
```

The dashboard should display useful information such as:

* Number of projects.
* Number of experiences.
* Pending testimonials.
* Unread messages.
* Published content.
* Draft content.

---

# 21. Content Publishing

Content should support publishing states.

At minimum:

```text
DRAFT
PUBLISHED
ARCHIVED
```

For testimonials:

```text
PENDING
APPROVED
REJECTED
PUBLISHED
```

Public APIs should only return content that should be publicly visible.

The frontend should never be responsible for deciding whether unpublished content is public.

That decision belongs to the backend.

---

# 22. API Architecture

The API should follow REST principles.

Example endpoints:

## Authentication

```text
POST /api/auth/login
POST /api/auth/logout
GET /api/auth/me
```

## Projects

```text
GET /api/projects
GET /api/projects/<slug>

POST /api/admin/projects
PATCH /api/admin/projects/<id>
DELETE /api/admin/projects/<id>
```

## Experience

```text
GET /api/experience

POST /api/admin/experience
PATCH /api/admin/experience/<id>
DELETE /api/admin/experience/<id>
```

## Skills

```text
GET /api/skills

POST /api/admin/skills
PATCH /api/admin/skills/<id>
DELETE /api/admin/skills/<id>
```

## Testimonials

```text
GET /api/testimonials

POST /api/testimonials/request
POST /api/testimonials/submit/<token>

PATCH /api/admin/testimonials/<id>
DELETE /api/admin/testimonials/<id>
```

## Contact

```text
POST /api/contact
GET /api/admin/contact-messages
PATCH /api/admin/contact-messages/<id>
```

The exact endpoint structure may be refined during implementation.

---

# 23. Backend Architecture

Use a modular Flask architecture.

Suggested structure:

```text
backend/
│
├── app/
│   ├── __init__.py
│   ├── config.py
│   ├── extensions.py
│   │
│   ├── models/
│   ├── schemas/
│   ├── routes/
│   ├── services/
│   ├── utils/
│   └── integrations/
│
├── migrations/
│
├── tests/
│
├── .env.example
├── requirements.txt
└── run.py
```

The exact structure may be adapted to the existing project architecture.

---

# 24. Frontend Architecture

Use a scalable React + TypeScript architecture.

Suggested structure:

```text
frontend/
│
├── src/
│   ├── assets/
│   ├── components/
│   ├── layouts/
│   ├── pages/
│   ├── routes/
│   ├── services/
│   ├── hooks/
│   ├── contexts/
│   ├── types/
│   ├── utils/
│   ├── features/
│   ├── App.tsx
│   └── main.tsx
│
└── ...
```

The architecture should avoid putting API calls directly inside every component.

API communication should be centralized through services.

---

# 25. TypeScript Requirements

TypeScript must be used properly.

Define interfaces/types for API data.

Examples:

```text
Project
Experience
Skill
Testimonial
Education
Certification
ContactMessage
SocialLink
User
```

Avoid using `any` unless there is a legitimate technical reason.

The frontend should receive strongly typed API responses.

---

# 26. Design Requirements

The portfolio should have a modern professional developer aesthetic.

The design should be:

* Clean.
* Responsive.
* Accessible.
* Professional.
* Fast.
* Modern.
* Visually distinctive without being excessive.

Tailwind CSS should be used for styling.

Avoid excessive animations.

Animations should improve usability rather than distract from content.

The design should prioritize:

1. Content.
2. Readability.
3. Navigation.
4. Performance.
5. Accessibility.

---

# 27. Responsive Design

The application must work across:

* Mobile.
* Tablet.
* Laptop.
* Desktop.
* Large screens.

The admin dashboard must also be responsive.

---

# 28. Accessibility

Follow basic WCAG principles.

The application should include:

* Semantic HTML.
* Keyboard navigation.
* Accessible forms.
* Labels for inputs.
* Appropriate ARIA attributes where necessary.
* Sufficient contrast.
* Focus states.
* Alternative text for images.
* Accessible navigation.

---

# 29. Security Requirements

Security must be considered from the beginning.

Requirements:

* Password hashing.
* JWT authentication.
* Authorization checks.
* Input validation.
* Server-side validation.
* Secure environment variables.
* CORS configuration.
* Secure cookies/storage strategy where applicable.
* Protection against unauthorized administrative actions.
* Secure testimonial invitation tokens.
* Rate limiting for public forms.
* File upload validation.
* Maximum upload sizes.
* Safe error responses.
* No secrets committed to Git.

Never trust data coming from the frontend.

All important validation must occur on the backend.

---

# 30. File Uploads

The application may eventually support:

* Profile image.
* Project screenshots.
* Company logos.
* Certificate files.
* CV files.

The architecture should not assume that files should permanently live inside the Git repository.

Use a storage abstraction.

This allows a future migration to:

* Cloudinary.
* AWS S3.
* Supabase Storage.
* Cloudflare R2.
* Other object storage.

The application should store file URLs or storage references in the database rather than raw binary files where appropriate.

---

# 31. Error Handling

The backend should return consistent API responses.

Example:

```json
{
  "success": false,
  "message": "Project not found"
}
```

Validation errors should clearly identify what went wrong.

The frontend should display user-friendly error messages rather than raw server errors.

---

# 32. Environment Configuration

Secrets must never be hardcoded.

Use:

```text
.env
```

for local development.

Provide:

```text
.env.example
```

with required variables but no secret values.

Potential variables include:

```text
FLASK_ENV
SECRET_KEY
DATABASE_URL
JWT_SECRET_KEY
MAIL_SERVER
MAIL_PORT
MAIL_USERNAME
MAIL_PASSWORD
FRONTEND_URL
```

Future integrations may add:

```text
LINKEDIN_CLIENT_ID
LINKEDIN_CLIENT_SECRET
LINKEDIN_REDIRECT_URI
```

These should only exist when LinkedIn integration is actually implemented.

---

# 33. Testing

The application should eventually include automated testing.

Backend:

* Unit tests.
* Model tests.
* Service tests.
* API tests.
* Authentication tests.
* Authorization tests.

Frontend:

* Component tests.
* Form tests.
* API interaction tests.
* Critical user-flow tests.

---

# 34. Deployment

## Frontend

Deploy to Vercel.

## Backend

Deploy Flask API to Render.

## Database

Use managed PostgreSQL.

Production environment variables must be configured through the hosting provider.

Never commit production secrets.

---

# 35. CI/CD

Future implementation should include GitHub Actions.

Potential pipeline:

```text
Git Push
   ↓
GitHub Actions
   ↓
Lint
   ↓
Tests
   ↓
Build
   ↓
Deploy
```

Pull requests should ideally run automated checks before merging.

---

# 36. SEO

The public portfolio should be optimized for search engines.

Include:

* Page titles.
* Meta descriptions.
* Semantic HTML.
* Open Graph metadata.
* Social sharing metadata.
* Descriptive URLs.
* Appropriate heading hierarchy.
* Sitemap.
* Robots configuration.

Project pages should have meaningful URLs such as:

```text
/projects/campuspulse
/projects/devcrypt
```

rather than:

```text
/projects/17
```

---

# 37. Performance

The application should prioritize performance.

Consider:

* Lazy loading.
* Image optimization.
* Code splitting.
* Efficient API requests.
* Caching where appropriate.
* Pagination for administrative data.
* Optimized database queries.
* Avoiding unnecessary React renders.

---

# 38. Scalability

The application should be designed so that adding new content does not require structural frontend changes.

For example, adding:

```text
Experience #4
```

should require a database/API operation rather than editing React source code.

Similarly:

```text
Project #10
```

should automatically appear using the existing project UI.

The system should be **data-driven rather than page-driven**.

---

# 39. Auditability

For important administrative operations, future versions should track:

* Created by.
* Updated by.
* Created date.
* Updated date.
* Published date.

This will make the system easier to audit and maintain.

---

# 40. Content Management Philosophy

The admin dashboard should behave like a lightweight CMS.

The administrator should be able to manage content without writing code.

For example:

```text
ADD PROJECT
       ↓
Fill form
       ↓
Save Draft
       ↓
Preview
       ↓
Publish
       ↓
Public portfolio updates
```

This principle should apply to:

* Projects.
* Experience.
* Skills.
* Testimonials.
* Certifications.
* Education.
* Profile information.

---

# 41. Future Multi-User Support

The initial application should have one administrator.

However, the authentication and authorization architecture should be designed so that additional roles can be introduced later.

Potential roles:

```text
ADMIN
EDITOR
REVIEWER
```

For example:

An editor might manage projects but not authentication.

A reviewer might approve testimonials.

An administrator could manage everything.

Do not implement unnecessary complexity in version 1, but avoid architectural decisions that make future role-based access impossible.

---

# 42. MVP Scope

The first production version should focus on:

### Public

* Home.
* About.
* Skills.
* Projects.
* Project details.
* Experience.
* Testimonials.
* Resume.
* Contact.
* Social links.
* Responsive UI.
* Dark/light mode.

### Admin

* Login.
* Dashboard.
* Project management.
* Experience management.
* Skill management.
* Testimonial management.
* Resume management.
* Contact messages.
* Profile management.

### Backend

* REST API.
* PostgreSQL.
* SQLAlchemy.
* Authentication.
* Authorization.
* Validation.
* Error handling.
* Migrations.

---

# 43. Post-MVP

After the MVP is stable, consider:

1. LinkedIn integration.
2. GitHub integration.
3. File storage.
4. Blog.
5. Analytics.
6. Newsletter.
7. Automated project synchronization.
8. CI/CD.
9. Advanced role management.
10. Content versioning.

Do not implement all post-MVP functionality before the core system is stable.

---

# 44. Development Philosophy

The project should be built incrementally.

Do not generate the entire codebase at once.

Implementation should follow dependency order.

For each file:

1. Explain why the file exists.
2. Explain its responsibility.
3. Explain its dependencies.
4. Explain how it communicates with other parts of the application.
5. Explain relevant engineering concepts.
6. Generate the complete code.
7. Explain the important sections.
8. Explain common mistakes.
9. Explain how the file can be extended later.

Generate one file at a time.

Do not silently create additional files.

Do not change the existing architecture without explaining why.

---

# 45. AI Development Instructions

This project will be developed using multiple AI assistants as development mentors.

The AI must not treat generated code as something to blindly copy.

The purpose is to help the developer understand the architecture and implementation.

When generating code:

* Explain decisions.
* Explain trade-offs.
* Prefer maintainable solutions.
* Avoid unnecessary abstraction.
* Avoid overengineering.
* Identify security concerns.
* Identify scalability concerns.
* Explain alternatives when relevant.
* Maintain consistency with previously generated code.

If an architectural decision is questionable, explicitly say so instead of blindly following it.

---

# 46. Important Implementation Rule

The developer has already created the project structure.

**Do not redesign the project structure unless there is a strong technical reason.**

First inspect the existing structure.

Then map the PRD requirements onto the existing architecture.

If something is missing, explain why it is necessary before introducing it.

---

# 47. Definition of Done

The MVP is considered complete when:

* The public portfolio is responsive.
* The frontend communicates with Flask.
* Flask communicates with PostgreSQL.
* Projects are stored in the database.
* Projects can be created from the admin dashboard.
* Projects can be edited.
* Projects can be deleted.
* Projects can be published/unpublished.
* Experience can be managed dynamically.
* Skills can be managed dynamically.
* Testimonials can be submitted through secure links.
* Testimonials require approval before publication.
* CV can be managed and downloaded.
* Contact messages can be submitted.
* Admin can view contact messages.
* Authentication protects the admin dashboard.
* Unauthorized users cannot access admin endpoints.
* Environment secrets are protected.
* Database migrations work.
* API errors are handled consistently.
* The application can be deployed to production.

---

# 48. Final Product

The final product should feel less like a static portfolio template and more like a small professional software platform.

The public visitor should see a polished developer portfolio.

The owner should see a private content-management dashboard.

Employers and professional contacts should have convenient ways to provide testimonials or interact with the portfolio.

The system should continue working as my career grows.

Adding:

* a new internship,
* a new job,
* a new project,
* a new certification,
* a new skill,
* a new testimonial,
* a new achievement,

should be a **content-management operation rather than a code change**.

The portfolio should therefore serve two purposes:

**Publicly:** demonstrate my engineering skills and professional experience.

**Internally:** provide a maintainable platform through which I can manage and grow my professional presence.
