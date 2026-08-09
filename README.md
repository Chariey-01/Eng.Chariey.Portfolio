# Eng.Chariey — Full Stack Developer Portfolio

> A modern, responsive, full-stack developer portfolio built from scratch with React, TypeScript, Tailwind CSS, and Flask.

This repository contains my personal developer portfolio, designed not only to showcase my projects and technical skills, but also to demonstrate how I approach software engineering, architecture, problem-solving, and building maintainable applications.

The portfolio is being built with a scalable architecture so that I can continue adding projects, features, content, and functionality as my engineering career develops.

---

##  Project Status

**Status:** In Development

This project is being built incrementally from the ground up.

The initial goal is to create a professional portfolio with a strong foundation that can later evolve into a more complete personal developer platform.

Planned future functionality includes project management, blog posts, analytics, an administration dashboard, GitHub integration, and other features.

---

##  Features

### Portfolio

* Professional landing page
* About Me section
* Technical skills
* Featured projects
* Complete project showcase
* Individual project details
* Project technology stacks
* GitHub repository links
* Live application links
* Project screenshots
* Project challenges and solutions
* Lessons learned
* Resume/CV download
* Contact form
* Social media links
* Responsive design
* Dark/light mode
* Custom 404 page

### Future Features

The architecture is intentionally designed to support future additions such as:

* Admin dashboard
* Authentication and authorization
* Blog/articles
* Certifications
* Testimonials
* GitHub API integration
* Automatic project synchronization
* Visitor analytics
* Search
* Project filtering
* Image management
* Resume version management
* Email notifications

---

#  Tech Stack

## Frontend

| Technology   | Purpose                                      |
| ------------ | -------------------------------------------- |
| React        | UI development                               |
| TypeScript   | Static typing and maintainable frontend code |
| Tailwind CSS | Styling and responsive UI                    |
| React Router | Client-side routing                          |
| Axios        | HTTP communication with the backend          |
| Vite         | Frontend development and build tooling       |

## Backend

| Technology               | Purpose                      |
| ------------------------ | ---------------------------- |
| Python                   | Backend programming language |
| Flask                    | Web framework                |
| Flask RESTful / REST API | API development              |
| SQLAlchemy               | ORM and database interaction |
| PostgreSQL               | Relational database          |
| Alembic / Flask-Migrate  | Database migrations          |
| Flask-CORS               | Cross-origin communication   |
| Flask-Mail               | Email functionality          |

## Deployment

| Service    | Purpose             |
| ---------- | ------------------- |
| Vercel     | Frontend deployment |
| Render     | Backend deployment  |
| PostgreSQL | Production database |

---

# Project Architecture

The application is divided into two primary systems:

```text
portfolio/
│
├── frontend/
│   ├── public/
│   └── src/
│
├── backend/
│   ├── app/
│   ├── migrations/
│   └── ...
│
├── .gitignore
├── README.md
└── ...
```

The frontend is responsible for the user interface and user interactions.

The Flask backend provides the API and handles application logic, data access, and communication with the database.

The separation allows both applications to evolve independently.

---

# 🖥️ Frontend Architecture

The frontend is built using React and TypeScript.

The frontend is responsible for:

* Rendering the user interface
* Client-side routing
* Displaying portfolio content
* Communicating with the Flask API
* Managing UI state
* Handling forms
* Providing responsive layouts
* Providing reusable components

The frontend follows a component-based architecture so that common UI elements can be reused throughout the application.

Examples include:

```text
Navbar
Footer
ProjectCard
ProjectGrid
SkillCard
Button
SectionHeader
ContactForm
```

This makes the application easier to maintain and extend.

---

# Backend Architecture

The backend is built using Flask and follows a modular architecture.

The backend is responsible for:

* Providing REST APIs
* Managing application configuration
* Database communication
* Business logic
* Contact form processing
* Project data
* Future authentication
* Future administration functionality

The backend is designed around separation of concerns.

Application responsibilities are separated into areas such as:

```text
config
extensions
models
routes
controllers
services
schemas
utils
```

This prevents the Flask application from becoming a single large file and makes future development easier.

---

#  Database

PostgreSQL will be used as the production relational database.

Potential entities include:

```text
Project
Skill
Category
ContactMessage
Resume
```

Additional models may be introduced as the application grows.

Database migrations will be handled through Flask-Migrate/Alembic rather than manually modifying the production database.

---

#  Projects

The portfolio will showcase applications that I have built throughout my software engineering journey.

## CampusPulse

**CampusPulse** is a full-stack campus discovery platform designed to help students discover useful places, services, facilities, and activities around campus.

### Technologies

* React
* JavaScript/TypeScript
* Flask
* PostgreSQL
* SQLAlchemy
* REST API
* Vercel
* Render

### Portfolio Showcase

The portfolio will provide:

* Project overview
* Problem being solved
* Key features
* Technical architecture
* Technologies used
* Development challenges
* Solutions
* Screenshots
* GitHub repository
* Live application

---

## DevCrypt

**DevCrypt** is an interactive cybersecurity challenge platform developed for a Moringa School career fair.

The application uses practical challenges to introduce participants to concepts involving programming, cryptography, configuration, databases, and security.

### Portfolio Showcase

The portfolio will document:

* Project purpose
* Architecture
* Challenge system
* Technologies used
* Development process
* Technical challenges
* Solutions
* Lessons learned
* GitHub repository
* Live application

---

## Aurelia Shopping App

A React-based shopping application created to practice frontend development, component architecture, routing, state management, and responsive interfaces.

### Technologies

* React
* JavaScript/TypeScript
* CSS/Tailwind CSS
* Vite

The portfolio will provide access to the deployed application and source code.

---

## Personal Coding Tracker

A personal productivity and learning application created to help track my software engineering learning journey, coding activities, and development progress.

The project represents an example of using software to solve a personal problem.

---

## Wordly

Wordly is a dictionary application and one of the earlier applications I built and shipped.

Although it is a simpler project compared with my newer applications, it represents an important stage in my development journey.

It may be included in the portfolio as part of my progression from beginner projects toward larger full-stack applications.

---

# Portfolio Goals

This portfolio has several goals.

### 1. Showcase Projects

Provide visitors with a clear understanding of what I have built and the technologies behind each project.

### 2. Demonstrate Engineering Ability

The portfolio itself will demonstrate:

* Clean architecture
* TypeScript
* React development
* API development
* Database design
* REST architecture
* Responsive UI development
* Git/GitHub workflow
* Deployment
* Maintainable code

### 3. Demonstrate Growth

The portfolio will show my progression as a software engineer rather than simply presenting a list of projects.

### 4. Provide Professional Contact

Potential employers, recruiters, collaborators, and other developers should be able to easily contact me.

---

#  Application Data Flow

The general architecture is:

```text
                 ┌──────────────────────┐
                 │       Visitor        │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │   React Frontend     │
                 │   TypeScript         │
                 │   Tailwind CSS       │
                 └──────────┬───────────┘
                            │
                         HTTP/REST
                            │
                            ▼
                 ┌──────────────────────┐
                 │    Flask Backend     │
                 │      REST API        │
                 └──────────┬───────────┘
                            │
                            ▼
                 ┌──────────────────────┐
                 │     PostgreSQL       │
                 └──────────────────────┘
```

The frontend should not directly communicate with the database.

All database operations go through the Flask API.

This creates a clear separation between the presentation layer, application layer, and data layer.

---

#  Security Considerations

Security will be considered throughout development.

Planned practices include:

* Environment variables for secrets
* No credentials committed to Git
* Secure password hashing if authentication is introduced
* Input validation
* API validation
* CORS configuration
* Secure production configuration
* Database connection security
* Protection against common web vulnerabilities
* Proper error handling
* Rate limiting where appropriate

Sensitive configuration will be stored in environment variables.

Example:

```env
DATABASE_URL=
SECRET_KEY=
MAIL_USERNAME=
MAIL_PASSWORD=
```

A `.env.example` file will document required variables without exposing their actual values.

---

#  Local Development

## Prerequisites

Before running the project locally, install:

* Git
* Python 3
* Node.js
* npm
* PostgreSQL

Verify your installations:

```bash
git --version
python3 --version
node --version
npm --version
psql --version
```

---

# Installation

Clone the repository:

```bash
git clone <https://github.com/Chariey-01/Eng.Chariey.Portfolio>
```

Move into the project:

```bash
cd portfolio
```

---

## Frontend Setup

Move into the frontend directory:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start the development server:

```bash
npm run dev
```

---

## Backend Setup

Move into the backend directory:

```bash
cd backend
```

Create a virtual environment:

```bash
python3 -m venv .venv
```

Activate it on Linux/macOS:

```bash
source .venv/bin/activate
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Create your environment file:

```bash
cp .env.example .env
```

Configure the required environment variables.

Then start the Flask development server.

---

#  Deployment

## Frontend

The React frontend will be deployed using Vercel.

The production frontend communicates with the deployed Flask API.

## Backend

The Flask backend will be deployed using Render.

The backend will connect to the production PostgreSQL database.

The general production architecture is:

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

---

#  Testing

Testing will be introduced as the application develops.

Planned areas include:

### Frontend

* Component testing
* Form validation testing
* UI behavior testing
* API integration testing

### Backend

* API endpoint testing
* Model testing
* Service testing
* Validation testing
* Error handling

Testing should be automated where practical.

---

# Future Improvements

The portfolio is intentionally designed to evolve.

Potential future improvements include:

* Admin dashboard
* Content management system
* Blog
* GitHub repository synchronization
* Automated project importing
* Analytics dashboard
* Visitor statistics
* Newsletter functionality
* Authentication
* Advanced project filtering
* Search
* Automated deployment pipelines
* Automated testing through CI/CD

These features will only be introduced when they provide meaningful value rather than adding unnecessary complexity.

---

#  Contributing

This is a personal portfolio project, so external contributions are not currently required.

However, constructive feedback, suggestions, and discussions are welcome.

---

# License

This project is primarily intended to showcase my personal work and software engineering journey.

Unless otherwise stated, the source code and original assets are not licensed for unrestricted reuse.

Please contact me before reusing substantial portions of the project.

---

#  About Me

I am a Computer Science learner and aspiring Full Stack Software Engineer focused on building practical, production-oriented applications.

My current technical interests include:

* Python
* Flask
* React
* TypeScript
* JavaScript
* SQL
* PostgreSQL
* REST APIs
* Software architecture
* Algorithms and data structures
* Full Stack development

This portfolio is part of my ongoing journey toward becoming a stronger and more capable software engineer.

---

#  Contact

For professional opportunities, collaboration, or questions:

**Email:** [charityjepkoech007@gmail.com]

**GitHub:** [https://github.com/Chariey-01]

**LinkedIn:** [https://www.linkedin.com/in/charity-jepkoech-91b5b6330]

**Portfolio:** []

---

#  Project Philosophy

> Build it. Understand it. Improve it.

This portfolio is not intended to be a static collection of links.

It is an evolving software project that reflects my growth as an engineer—from early applications to increasingly complex full-stack systems.

The goal is to continuously improve the architecture, user experience, code quality, accessibility, performance, and overall engineering practices behind it.
