# FastAPI Book Project

This FastAPI application allows users to retrieve book details by ID. It is deployed with a CI/CD pipeline using GitHub Actions and is served using Nginx as a reverse proxy.

---

## Features
- Retrieve book details by ID.
- Error handling for non-existent book IDs.

---

## Endpoint Specification
### GET `/api/v1/books/{book_id}`  
**Parameters:**  
- `book_id`: (integer) ID of the book.  

**Response:**  
- `200 OK`: Returns JSON with the book details.  
- `404 Not Found`: Returns an error message if the book does not exist:  
  ```json
  {
    "detail": "Book not found"
  }
  ```

  ## Tech Stack
- **FastAPI**: For building the backend.
- **Nginx**: Used as a reverse proxy.
- **GitHub Actions**: For CI/CD pipeline.

## Getting Started
### Installation

1. **Clone the Repository:**
```bash
 git clone https://github.com/your-username/fastapi-book-project
 cd fastapi-book-project
 ```

 2. **Create and Activate a Virtual Environment:**
```bash
python3 -m venv venv
source venv/bin/activate
```

3. **Install Dependencies:**
```bash
pip install -r requirements.txt
```

## Running the Application Locally
 **Start the FastAPI server:**
```bash
uvicorn app.main:app --reload
```

## Running Tests
 **The CI pipeline uses pytest to run tests. To manually run tests locally:**
```bash
pytest
```
 
 ## CI/CD Pipeline
This project uses **GitHub Actions** for CI/CD:

- **CI Pipeline:**  
  - Runs on pull requests to the main branch.  
  - Executes `pytest` to run tests.  
  - Fails if any test does not pass.  

- **CD Pipeline:**  
  - Triggers on merging a pull request to the main branch.  
  - Automatically deploys the latest changes.