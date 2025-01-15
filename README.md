# Hybrid IDE Project

## Overview

The Hybrid IDE project is a Python-exclusive development environment designed to run locally. It integrates a modern, customizable editor with debugging capabilities, hidden test cases, and an AI assistant for concise guidance. It supports a hybrid architecture: a desktop application for ease of use, paired with a browser-based interface for flexibility.

## Features

1. Code Editing: Syntax highlighting, auto-formatting, and proper spacing powered by Monaco Editor.
2. Debugging and Execution: Run Python code and access hidden test cases directly from the IDE.
3. Customizable Themes: Toggle between light, dark, potentially other modes. Focus on default light, modern mode, matching complement dark mode.
4. Problem Selection:
   - Problem type and difficulty.
   - Problem mutation for generating variations.
   - Database toggle:
     - Experimental AI Mode: Let the AI generate problems dynamically.
     - Validated DB Mode: Retrieve problems from the validated database.
     - For DB: 
       - Problem Type
       - Problem Difficulty
       - Problem Statement
       - Hidden Test Cases
       - Common structure for all problems so others can enter their own problems
5. AI Assistant:
   - Concise explanations and suggestions.
   - No direct code modification, function suggestion possible.
   - Context-aware suggestions based on the editor and chat input.
6. Hybrid Architecture:
   - Electron.js to bundle the backend and frontend into a local desktop application.
   - React-based web interface accessible via a local browser.

## Technologies

### Frontend
- Framework: React
- Editor: Monaco Editor
- Styling: Tailwind CSS

### Backend
- Framework: FastAPI or Flask
- Execution Environment: Python runtime (using exec or isolated containers like Docker if needed)

### AI Integration
- Model: Ollama (local) for:
  - Code assistance
  - Text embeddings (using codellama or nomic-embed)
  - Problem similarity matching
- Features:
  - Semantic problem search using local embeddings
  - Similar problem recommendations
  - Difficulty estimation
  - Problem variation generation
- Benefits:
  - Fully local processing
  - No API costs
  - Privacy-focused
  - Customizable models

### Database
- Supabase (PostgreSQL + pgvector)
  - Problems Table:
    - id: uuid
    - title: text
    - description: text
    - difficulty: enum
    - type: enum
    - test_cases: jsonb
    - embedding: vector(768)  // Dimension depends on chosen Ollama model
  - User Solutions Table:
    - id: uuid
    - user_id: uuid (foreign key)
    - problem_id: uuid (foreign key)
    - solution: text
    - language: enum
    - status: enum
  - Problem Categories Table:
    - id: uuid
    - name: text
    - description: text

### Desktop Application
- Framework: Electron.js

## File Structure

project-root/
- frontend/
  - public/
  - src/
    - components/
    - pages/
    - styles/
    - App.js
    - index.js
  - package.json
- backend/
  - app/
    - main.py
    - routers/
    - models/
    - utils/
  - tests/
  - requirements.txt
- electron/
  - main.js
  - preload.js
  - package.json
- database/
  - problems.db
- .gitignore
- README.md
- LICENSE

### Initialize the Project Structure

- Use the file structure above to set up your project.
- Create necessary folders and files using mkdir and touch commands or a preferred IDE.

### Set Up Frontend

Run the following commands:

- `cd frontend`
- `npx create-react-app .`
- `npm install monaco-editor tailwindcss`

### Set Up Backend

Run the following commands:

- `cd backend`
- `python3 -m venv venv`
- `source venv/bin/activate` (or `venv\Scripts\activate` on Windows)
- `pip install fastapi uvicorn sqlite3`

### Set Up Electron

Run the following commands:

- `cd electron`
- `npm init -y`
- `npm install electron`

### Link Frontend and Backend

- In Electron, configure main.js to start the backend server and open the React app.