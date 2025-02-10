# FastAPI Book Project

This repository is a FastAPI-based API for managing books. It demonstrates RESTful API principles along with a complete CI/CD pipeline using GitHub Actions and automated deployment on Render and/or a Windows server with Nginx as a reverse proxy. This project was built as part of the HNG12 DEVOPS x BACKEND Stage 2 challenge.

## Table of Contents

- [FastAPI Book Project](#fastapi-book-project)
  - [Table of Contents](#table-of-contents)
  - [Overview](#overview)
  - [Features](#features)
  - [Project Structure](#project-structure)
  - [Setup and Installation](#setup-and-installation)
    - [Prerequisites](#prerequisites)
    - [Local Setup](#local-setup)
  - [Running the Application Locally](#running-the-application-locally)
  - [API Endpoints](#api-endpoints)
    - [Health Check](#health-check)
    - [Books Endpoints](#books-endpoints)
  - [CI/CD Pipelines](#cicd-pipelines)
  - [Deployment](#deployment)
    - [Deploying on Render](#deploying-on-render)
    - [Deploying on a Windows Server with Nginx](#deploying-on-a-windows-server-with-nginx)
  - [Collaborators](#collaborators)
  - [Contributing](#contributing)
  - [License](#license)

## Overview

The FastAPI Book Project provides a RESTful API to perform CRUD operations on a collection of books stored in an in-memory database. It includes a missing endpoint to retrieve a specific book by its ID, robust error handling, and automated testing and deployment pipelines.

## Features

- **RESTful API** built with FastAPI
- **CRUD Operations:** Create, retrieve, update, and delete books
- **In-Memory Database:** For demonstration purposes
- **CI/CD Pipelines:** Automated testing on pull requests and deployment on pushes to the `main` branch via GitHub Actions
- **Deployment:** Can be deployed on Render or a Windows server with Nginx as a reverse proxy
- **CORS Enabled:** All origins allowed
- **Environment Configurable:** Using environment variables and a configuration file

## Project Structure

```
fastapi-book-project/
├── api/
│   ├── __init__.py
│   ├── main.py                # Entry point for the FastAPI app
│   ├── router.py              # API router configuration
│   ├── endpoints/
│   │   └── books.py           # Book endpoints (CRUD operations)
│   └── db/
│       └── schemas.py         # Models (Book, Genre) and InMemoryDB
├── core/
│   └── config.py              # Application settings
├── tests/
│   └── ...                    # Pytest tests for the application
├── .github/
│   └── workflows/
│       ├── ci.yml             # CI pipeline configuration (runs tests)
│       └── deploy.yml         # CD pipeline configuration (deployment)
├── requirements.txt           # Python dependencies
├── runtime.txt                # Python runtime version (e.g., python-3.10.9)
└── README.md                  # This file
```

## Setup and Installation

### Prerequisites

- **Python 3.10+**
- **Git**

### Local Setup

1. **Clone the Repository:**

   ```bash
   git clone https://github.com/Layconnn/fastapi-book-project.git
   cd fastapi-book-project
   ```

2. **Create a Virtual Environment:**

   ```bash
   python -m venv venv
   ```

3. **Activate the Virtual Environment:**

   - **Windows:**
     ```bash
     venv\Scripts\activate
     ```
   - **macOS/Linux:**
     ```bash
     source venv/bin/activate
     ```

4. **Install Dependencies:**
   ```bash
   pip install --upgrade pip
   pip install -r requirements.txt
   ```

## Running the Application Locally

To run the FastAPI application locally:

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Open your browser and navigate to [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) to access the interactive API documentation.

## API Endpoints

### Health Check

- **GET** `/healthcheck`  
  **Response:**
  ```json
  { "status": "active" }
  ```

### Books Endpoints

- **Create a Book**  
  **POST** `/api/v1/books/`  
  **Request Body:** JSON object representing the book  
  **Response:** Created book details (HTTP 201)

- **Get All Books**  
  **GET** `/api/v1/books/`  
  **Response:** JSON object containing all books

- **Get a Specific Book**  
  **GET** `/api/v1/books/{book_id}`  
  **Response:** JSON with the book details

- **Update a Book**  
  **PUT** `/api/v1/books/{book_id}`  
  **Response:** Updated book details

- **Delete a Book**  
  **DELETE** `/api/v1/books/{book_id}`  
  **Response:** HTTP 204 (No Content)

## CI/CD Pipelines

This project includes GitHub Actions workflows for automated testing and deployment.

## Deployment

### Deploying on Render

1. **Create a New Web Service on Render**
2. **Set the Start Command:**
   ```bash
   uvicorn main:app
   ```
3. **Deploy & Access API:**
   Use the provided Render URL (e.g., `https://your-app-name.onrender.com/api/v1/books/2`).

### Deploying on a Windows Server with Nginx

1. **Ensure Public Accessibility & Install Nginx**
2. **Configure Nginx as a Reverse Proxy:**

   ```nginx
   server {
       listen 80;
       server_name your_public_ip_or_domain;

       location / {
           proxy_pass http://127.0.0.1:8000;
           proxy_set_header Host $host;
           proxy_set_header X-Real-IP $remote_addr;
           proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
       }
   }
   ```

3. **Reload Nginx & Verify API Access**

## Collaborators

- # hng12-devbotops

## Contributing

Contributions are welcome! Please open an issue or submit a pull request.

## License

This project is licensed under the [MIT License](LICENSE).

Happy coding.
