# Pangsa Kerja

Pangsa Kerja is a web application designed to assist job seekers with CV analysis and interview preparation, specifically featuring a Kraepelin test.

This repository contains both the FastAPI backend and a simple HTML/JavaScript frontend.

## Table of Contents

* [Features](#features)
* [Getting Started](#getting-started)
    * [Prerequisites](#prerequisites)
    * [Backend Setup](#backend-setup)
    * [Frontend Setup](#frontend-setup)
* [Usage](#usage)
* [API Endpoints](#api-endpoints)
* [Testing](#testing)
* [Technologies Used](#technologies-used)
* [License](#license)

## Features

* **CV Analysis:** Upload your CV (PDF, DOC, DOCX) and get an AI-powered analysis including a score, strengths, weaknesses, recommendations, and certification suggestions.
* **Kraepelin Test:** Practice the Kraepelin (addition) test to improve concentration and numerical skills, often used in recruitment processes.
* **User Management:** Basic user creation and management for CV analysis.
* **Admin Dashboard:** View statistics like total users, CV analyses, and Kraepelin tests (backend only).
* **User Data Export:** Export user data for B2B prospects (backend only).

## Getting Started

Follow these instructions to set up and run the Pangsa Kerja application locally.

### Prerequisites

* Python 3.8+
* pip (Python package installer)
* Git
* A web browser

### Backend Setup

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/your-username/pangsa-kerja.git](https://github.com/your-username/pangsa-kerja.git)
    cd pangsa-kerja/backend
    ```

2.  **Run the setup script:**
    The `setup.sh` script will create a virtual environment, install dependencies, set up the `.env` file, and initialize the database.

    ```bash
    chmod +x setup.sh
    ./setup.sh
    ```
    * **Note:** If you are on Windows, you might need to run the commands inside `setup.sh` manually or use Git Bash/WSL.
    * The script will prompt you to edit the `.env` file.

3.  **Configure Environment Variables:**
    Open the newly created `.env` file in the `backend/` directory and update the following:
    * `ANTHROPIC_API_KEY`: Get your API key from Anthropic.
    * `SECRET_KEY`: Generate a strong, random string for JWT.
    * `DATABASE_URL`: By default, it uses SQLite. For PostgreSQL or MySQL, uncomment and configure the respective lines.

    Example `.env` content:
    ```
    # .env file - Environment Configuration

    # Database Configuration
    DATABASE_URL=sqlite:///./pangsa_kerja.db
    # For PostgreSQL: postgresql://username:password@localhost/pangsa_kerja
    # For MySQL: mysql+pymysql://username:password@localhost/pangsa_kerja

    # Anthropic Claude API
    ANTHROPIC_API_KEY=your-anthropic-api-key-here # <--- IMPORTANT: Replace with your key

    # JWT Configuration
    SECRET_KEY=your-super-secret-jwt-key-here # <--- IMPORTANT: Replace with a strong key
    ALGORITHM=HS256
    ACCESS_TOKEN_EXPIRE_MINUTES=30

    # File Upload Configuration
    MAX_FILE_SIZE=5242880  # 5MB in bytes
    UPLOAD_FOLDER=./uploads

    # CORS Configuration
    ALLOWED_ORIGINS=http://localhost:3000,http://localhost:8080,http://localhost:8000 # Add your frontend origin
    # If running frontend from file system, you might need to allow "*" during development, but adjust for production.

    # Logging
    LOG_LEVEL=INFO
    LOG_FILE=./logs/app.log

    # Email Configuration (for notifications)
    SMTP_SERVER=smtp.gmail.com
    SMTP_PORT=587
    SMTP_USERNAME=your-email@gmail.com
    SMTP_PASSWORD=your-app-password
    ```

4.  **Activate Virtual Environment:**
    ```bash
    source venv/bin/activate # On Windows: venv\Scripts\activate
    ```

5.  **Run the Backend Server:**
    ```bash
    python main.py
    ```
    The FastAPI application will start on `http://localhost:8000`. You can access the API documentation at `http://localhost:8000/docs`.

### Frontend Setup

The frontend is a static HTML file.

1.  **Navigate to the frontend directory:**
    ```bash
    cd ../frontend
    ```

2.  **Open `index.html`:**
    Simply open the `index.html` file in your web browser.
    ```bash
    # On macOS
    open index.html
    # On Windows
    start index.html
    # On Linux (often)
    xdg-open index.html
    ```
    Alternatively, you can serve it with a simple HTTP server (e.g., Python's `http.server`):
    ```bash
    python -m http.server 8080
    ```
    Then, open your browser to `http://localhost:8080/`.

## Usage

* **Home Page:** Provides an overview and links to the main features.
* **Poles CV (CV Polish):**
    * Click "Poles CV" from the navigation or home page.
    * Click the "Upload CV" area to select a PDF, DOC, or DOCX file (max 5MB).
    * Fill in your personal information (Name, Email, Phone, Years of Experience, Skills).
    * Click "Analisis CV" to get AI-powered feedback.
* **Persiapan Interview (Interview Preparation - Kraepelin Test):**
    * Click "Interview Prep" from the navigation or home page.
    * Select your desired test duration (1, 2, or 5 minutes).
    * Read the instructions and click "Mulai Tes".
    * Enter the last digit of the sum of the two numbers displayed and press Enter.
    * After the timer runs out, your test results and a performance chart will be displayed.

## API Endpoints

The backend provides the following REST API endpoints:

* `GET /`: Basic API status.
* `GET /health`: Health check endpoint.
* `POST /api/users`: Create a new user.
* `POST /api/cv/analyze`: Upload and analyze a CV with AI.
* `POST /api/kraepelin/save-result`: Save Kraepelin test results.
* `GET /api/users/{user_id}/cv-analyses`: Get all CV analyses for a specific user.
* `GET /api/stats/dashboard`: Get dashboard statistics (total users, CV analyses, Kraepelin tests, average CV score).
* `GET /api/users/export`: Export all user data.

Refer to `http://localhost:8000/docs` for detailed interactive API documentation (Swagger UI).

## Testing

You can test the backend API using the provided `test_api.py` script.

1.  Ensure the backend server is running.
2.  Activate the virtual environment:
    ```bash
    cd backend
    source venv/bin/activate
    ```
3.  Run the tests:
    ```bash
    python tests/test_api.py
    ```

The `test_api.py` script will print the responses from each endpoint. It also includes `curl` examples for manual testing.

## Technologies Used

### Backend
* **FastAPI:** Web framework for building APIs.
* **Uvicorn:** ASGI server for running FastAPI.
* **SQLAlchemy:** ORM for database interactions.
* **SQLite (Default):** Lightweight file-based database.
* **PyPDF2:** For PDF text extraction.
* **python-docx:** For DOCX text extraction.
* **Anthropic Claude API:** For AI-powered CV analysis.
* **Pydantic:** Data validation and settings management.

### Frontend
* **HTML5:** Structure of the web page.
* **CSS3:** Styling.
* **JavaScript:** Client-side logic for interactions, form handling, and Kraepelin test.
* **Chart.js (simulated in JS):** For drawing the Kraepelin performance chart.

## License

This project is open source and available under the MIT License.
