POETRY := poetry

.PHONY: install run test lint format check docker-build docker-run

install:
	$(POETRY) install

run:
	$(POETRY) run uvicorn app.main:app --reload --host 0.0.0.0 --port 8000

test:
	$(POETRY) run pytest

lint:
	$(POETRY) run ruff check .

format:
	$(POETRY) run ruff format .

check: lint test

docker-build:
	docker build -t job-search-assistant-backend .

docker-run:
	docker run --rm -p 8000:8000 job-search-assistant-backend
