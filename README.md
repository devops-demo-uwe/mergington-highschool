# Mergington High School Activities

Mergington High School Activities is a small FastAPI demo application for
browsing extracurricular activities and signing students up for them. It
includes a JSON API and a browser-based interface served by the same
application.

This demo is designed to showcase AI-assisted coding practices. It
intentionally includes bugs and other shortcomings so they can be identified
and fixed using AI coding tools. The project was spun off from the official
GitHub Skills exercise.

## Features

- View available activities, schedules, and remaining capacity
- Sign up for an activity with a student email address
- Explore the API through automatically generated OpenAPI documentation
- Serve the frontend and API from one FastAPI process

## Requirements

- Python 3.10 or later
- `pip`

## Run locally

1. Create and activate a virtual environment:

   ```powershell
   python -m venv .venv
   .\.venv\Scripts\Activate.ps1
   ```

2. Install the dependencies:

   ```powershell
   python -m pip install -r requirements.txt
   ```

3. Start the development server:

   ```powershell
   python -m uvicorn src.app:app --reload
   ```

4. Open one of the following URLs:

   - Web application: http://localhost:8000
   - Swagger UI: http://localhost:8000/docs
   - ReDoc: http://localhost:8000/redoc

The included VS Code launch configuration can also start the application with
the **Launch Mergington WebApp** debug profile.

## API

### List activities

```http
GET /activities
```

Returns an object keyed by activity name. Each activity contains its
description, schedule, maximum number of participants, and current participant
email addresses.

### Sign up for an activity

```http
POST /activities/{activity_name}/signup?email={student_email}
```

Example:

```powershell
curl.exe -X POST "http://localhost:8000/activities/Chess%20Club/signup?email=student@mergington.edu"
```

The endpoint returns `404 Not Found` when the requested activity does not
exist.

## Project structure

```text
.
|-- src/
|   |-- app.py              # FastAPI application and in-memory data
|   `-- static/
|       |-- index.html      # Browser interface
|       |-- app.js          # API integration and form handling
|       `-- styles.css      # Page styling
|-- requirements.txt
`-- pytest.ini
```

## Data storage

Activity and signup data is stored in memory. Changes are available only while
the server is running and are reset whenever the application restarts.
