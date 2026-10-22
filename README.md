# Job Search Assistant

An agentic backend that helps automate the job search workflow. The system is
designed to discover new roles, compare them with a user's CV, improve the CV
for relevant opportunities, and draft tailored outreach emails and application
materials.

## Current Status

The project currently contains the FastAPI backend foundation, including a
health endpoint, Poetry dependency management, Ruff linting, pytest, and a
Docker image. The multi-agent workflow will be built on top of this foundation.

## Planned Workflow

The backend is intended to coordinate focused agents rather than put the whole
workflow in one large process:

1. **Job discovery** searches configured job boards, company pages, and other
	sources for new opportunities.
2. **Job normalization** cleans and deduplicates job postings so they can be
	compared consistently.
3. **CV matching** ranks roles against the user's experience, skills, and
	preferences.
4. **CV tailoring** updates or creates a role-specific CV while preserving the
	user's factual background.
5. **Email and application writing** drafts personalized recruiter emails,
	cover letters, and other application content.
6. **Review and delivery** presents the results for user approval before any
	external message is sent or application is submitted.

Human approval should remain part of the workflow before sending emails,
editing the source CV, or submitting an application.

## Backend Development

Requirements:

- Python 3.12+
- Poetry 2+
- Docker, for containerized development and deployment

Install dependencies and start the API from `backend/`:

```bash
cd backend
make install
make run
```

The API is available at `http://localhost:8000`.

- Health check: `http://localhost:8000/health`
- Interactive API docs: `http://localhost:8000/docs`

Run the backend quality checks:

```bash
cd backend
make check
```

Format the code with Ruff:

```bash
cd backend
make format
```

## Docker

Build and run the backend container:

```bash
cd backend
make docker-build
make docker-run
```

The Docker image exposes port `8000`.

## Project Structure

```text
.
├── backend/
│   ├── app/
│   │   └── main.py       # FastAPI application entrypoint
│   ├── tests/             # Backend tests
│   ├── Makefile
│   ├── Dockerfile
│   ├── poetry.lock
│   └── pyproject.toml
├── frontend/              # Next.js and shadcn frontend
│   ├── app/
│   ├── components/
│   ├── .gitignore
│   └── package.json
├── .vscode/
│   └── settings.json      # Hide generated Python files in VS Code
├── Makefile
└── README.md
```

The backend and frontend each own their ignore file. Generated Python files
such as `__pycache__`, `.pyc`, `.pytest_cache`, and `.ruff_cache`, as well as
Node and Next.js output such as `node_modules` and `.next`, stay scoped to the
appropriate project and are hidden from the VS Code Explorer and Search view.