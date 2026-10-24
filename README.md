# Trusted Alumni Communication and Career Networking Portal

A Flask-based web application designed to help alumni and administrators communicate, share career opportunities, and build a trusted alumni network. The application has separate portals for **ANSA (administrator)** and **VANM (alumni/member)** users and stores application records in an LMDB database.

## Features

### Administrator portal (ANSA)
- Administrator registration and login.
- Password hashing for account credentials.
- Dashboard with member-related information.
- Review pending alumni/member registrations and approve or reject them.
- Browse the member directory.
- Create and manage announcements.
- Create and manage job postings.
- View analytics.

### Alumni/member portal (VANM)
- Member registration and login.
- Profile viewing and updating.
- Alumni directory.
- Browse career opportunities and job postings.
- Apply for a posted job.
- Session-based access to protected pages.

### Application and interface
- Flask routes and Jinja2 HTML templates.
- Shared base template and separate administrator/member page templates.
- Custom CSS styling for a consistent, responsive interface.
- CSRF-token validation for form submissions where implemented.
- LMDB key-value storage for application records.

## Tech stack

- **Python**
- **Flask** — web application and routing
- **Jinja2** — HTML templating (included with Flask)
- **LMDB** (`lmdb` Python package) — local key-value database
- **Werkzeug security utilities** — password hashing and verification
- **HTML/CSS** — user interface

## Project structure

```text
Trusted-Alumni-Communication-and-Career-Networking/
├── app.py
├── main.py
├── run3120.bat
├── static/
│   └── style.css
├── templates/
│   ├── base.html
│   ├── index.html
│   ├── ansa/
│   │   ├── analytics.html
│   │   ├── announcements.html
│   │   ├── dashboard.html
│   │   ├── job_postings.html
│   │   ├── login.html
│   │   ├── member_directory.html
│   │   ├── pending_registrations.html
│   │   └── signup.html
│   └── vanm/
│       ├── alumni_directory.html
│       ├── career_opportunities.html
│       ├── dashboard.html
│       ├── login.html
│       ├── profile.html
│       └── signup.html
└── README.md
```

The LMDB database files are created/used separately from the source code. Do not commit live database files or database lock files to a public repository.

## Requirements

- Python 3.9 or later recommended
- `Flask`
- `lmdb`
- `Werkzeug` (installed as a Flask dependency)

## Run locally

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
cd <YOUR_REPOSITORY_FOLDER>
```

Replace the placeholders with your actual GitHub repository URL and folder name.

### 2. Create and activate a virtual environment

**Windows (PowerShell):**
```powershell
py -m venv .venv
.\.venv\Scripts\Activate.ps1
```

**Windows (Command Prompt):**
```bat
py -m venv .venv
.venv\Scripts\activate.bat
```

**macOS/Linux:**
```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install Flask lmdb
```

You can save the installed dependencies for repeatable setup with:

```bash
python -m pip freeze > requirements.txt
```

### 4. Configure the session secret

The application reads `SESSION_SECRET` from the environment. Set a unique secret before running it.

**Windows PowerShell:**
```powershell
$env:SESSION_SECRET = "replace-with-a-long-random-secret"
```

**Windows Command Prompt:**
```bat
set SESSION_SECRET=replace-with-a-long-random-secret
```

**macOS/Linux:**
```bash
export SESSION_SECRET="replace-with-a-long-random-secret"
```

If `SESSION_SECRET` is not set, the current source code falls back to a hard-coded development key. Set the environment variable for normal use, and change the fallback in the source before deploying publicly.

### 5. Start the application

From the directory containing `app.py`, run:

```bash
python app.py
```

Open the local address shown in the terminal (commonly `http://127.0.0.1:5000/`).

If the application does not start, check the terminal error and confirm that the dependencies installed successfully. The included `main.py` is a simple placeholder; `app.py` is the Flask application entry point.

## Database configuration

The application uses LMDB. By default, it stores its database at:

```text
./alumni_nexus.lmdb
```

You can set a different path using the `LMDB_PATH` environment variable before starting the application. The database is intended to be local runtime data; keep user records and database/lock files out of source control.

## Important security notes

This project is a prototype and should be reviewed before production deployment.

- Set a strong, private `SESSION_SECRET`; never publish real secrets.
- Do not commit personal data, credentials, live LMDB files, or lock files.
- Passwords and security answers are hashed in the application, but authentication and account-recovery flows still need a full security review.
- Review authorization checks, CSRF coverage, input validation, error handling, session settings, and production HTTPS configuration before deployment.
- The current source sets `SESSION_COOKIE_SECURE = False`, which is suitable only for local HTTP testing. Configure secure cookies and HTTPS for production.
- Use synthetic test data in public demonstrations.

## Future enhancements

- Add automated tests and CI checks.
- Add email verification and secure account-recovery workflows.
- Improve role-based authorization and audit logging.
- Add pagination and search/filtering to directories and job listings.
- Add deployment configuration and production server setup.
- Document screenshots and a demo walkthrough.

## Contribution

1. Fork the repository.
2. Create a feature branch.
3. Make and test your changes.
4. Submit a pull request describing the change.

## License

No license file was included in the supplied project archive. Add a `LICENSE` file if you intend to specify how others may use, modify, or distribute this project.
