# Transcriber App

A full-stack web application for transcribing audio files into text using state-of-the-art speech recognition models.

## Overview

Transcriber App provides a clean web interface for uploading audio files and receiving accurate text transcriptions. The backend leverages Hugging Face Transformers and PyTorch for high-quality, on-device speech recognition, with Celery and Redis handling asynchronous task processing to keep the UI responsive during long transcriptions.

## Tech Stack

**Frontend**
- React + TypeScript
- Vite
- ESLint

**Backend**
- FastAPI (Python 3.10)
- Celery + Redis (async task queue)
- SQLModel + SQLite (data persistence)
- Hugging Face Transformers + PyTorch (speech recognition)
- Docker + Docker Compose

## Getting Started

### Prerequisites

- Node.js ≥ 18
- Docker + Docker Compose

### Frontend

```bash
cd frontend
npm install
npm run dev
```

The dev server will start at `http://localhost:5173`.

### Backend

```bash
cd backend
docker-compose up --build
```

Docker Compose will spin up the FastAPI server, Celery worker, and Redis broker together.

## Architecture

The application follows a decoupled architecture:

1. **Client** uploads an audio file via the React frontend
2. **FastAPI** receives the file and enqueues a transcription task via Celery
3. **Celery worker** runs the Transformers-based speech recognition model
4. **Result** is stored in SQLite and returned to the client

## Project Structure

```
transcriber-app/
├── frontend/          # React + TypeScript app
│   ├── src/
│   └── vite.config.ts
└── backend/           # FastAPI service
    ├── src/
    ├── main.py
    ├── Dockerfile
    └── docker-compose.yml
```
