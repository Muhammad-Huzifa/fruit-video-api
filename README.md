# FruitVideo AI

[![CI](https://github.com/Muhammad-Huzifa/fruit-video-api/actions/workflows/ci.yml/badge.svg)](https://github.com/Muhammad-Huzifa/fruit-video-api/actions/workflows/ci.yml)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB.svg)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-API-009688.svg)](https://fastapi.tiangolo.com/)

FruitVideo AI is a clean FastAPI backend foundation for turning a text prompt into a
fruit-focused video. It provides validated API endpoints, interactive documentation,
automated tests, continuous integration, and Docker support.

> **Current status:** This repository is an API prototype. The `/generate` endpoint
> validates the prompt and returns a public demonstration video. It does not generate
> a new AI video yet. The service layer is ready to be connected to a real model.

## Features

- FastAPI backend with automatic Swagger documentation
- Validated prompt input using Pydantic
- Health endpoint for deployment monitoring
- Separate application, schema, and service layers
- Automated API tests and GitHub Actions checks
- Docker configuration for consistent deployment
- Backward compatibility with the original `backend.py` entry point

## Project structure

```text
FruitVideo_AI/
├── .github/workflows/ci.yml   # Automated quality checks and tests
├── app/
│   ├── __init__.py            # Package version
│   ├── main.py                # FastAPI application and routes
│   ├── schemas.py             # Request and response models
│   └── services.py            # Video-generation service layer
├── tests/test_api.py          # API tests
├── backend.py                 # Compatible legacy entry point
├── Dockerfile                 # Container configuration
├── requirements.txt           # Runtime dependencies
├── requirements-dev.txt       # Development dependencies
└── pyproject.toml             # Test and lint configuration
```

## Quick start

### 1. Clone the repository

```bash
git clone https://github.com/Muhammad-Huzifa/fruit-video-api.git
cd fruit-video-api
```

### 2. Create and activate a virtual environment

Windows Git Bash:

```bash
python -m venv .venv
source .venv/Scripts/activate
```

macOS or Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
```

### 3. Install dependencies

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### 4. Start the API

```bash
uvicorn app.main:app --reload
```

Open these addresses in your browser:

- API: <http://127.0.0.1:8000>
- Interactive documentation: <http://127.0.0.1:8000/docs>
- Alternative documentation: <http://127.0.0.1:8000/redoc>

## API endpoints

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `GET` | `/` | Show API information |
| `GET` | `/health` | Check service health |
| `POST` | `/generate` | Validate a prompt and return the demo video |

### Example generation request

```bash
curl -X POST "http://127.0.0.1:8000/generate" \
  -H "Content-Type: application/json" \
  -d '{"prompt":"A fresh red apple rotating slowly on a wooden table"}'
```

Example response:

```json
{
  "status": "success",
  "prompt": "A fresh red apple rotating slowly on a wooden table",
  "video_url": "https://www.w3schools.com/html/mov_bbb.mp4",
  "demo": true,
  "message": "Demo response returned; AI model integration is the next step."
}
```

## Run quality checks

Install the development tools and run the checks:

```bash
python -m pip install -r requirements-dev.txt
ruff check .
ruff format --check .
pytest
```

## Run with Docker

```bash
docker build -t fruitvideo-ai .
docker run --rm -p 8000:8000 fruitvideo-ai
```

## Next development steps

- Connect the service layer to a real text-to-video model
- Return job IDs for long-running video generation
- Add model and storage configuration through environment variables
- Store generated videos locally or in cloud object storage
- Add authentication, rate limiting, and deployment monitoring

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for the local development workflow.

## Author

**Muhammad Huzifa** — [GitHub profile](https://github.com/Muhammad-Huzifa)
