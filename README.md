# **FastAPI Book Project**  

### **Overview**  
This project is a FastAPI application for managing books, deployed using **Railway** with a **CI/CD pipeline** via **GitHub Actions** and served with **Nginx**.  

---

## **Setup Instructions**  

### **1. Clone the Repository**  
```sh
git clone https://github.com/YOUR_USERNAME/fastapi-book-project.git
cd fastapi-book-project
```

### **2. Install Dependencies**  
Ensure you have Python 3.11+ installed, then run:

```sh
pip install -r requirements.txt
```

### **3. Run the Application Locally**
```sh
uvicorn main:app --host 0.0.0.0 --port 8000 --reload
```
Then visit: http://localhost:8000/docs to see the API documentation.


## **Deployment Instructions**  

### **1. Deploying to Railway**  
1. **Log in to [Railway](https://railway.app/)** and create a new project.  
2. **Link your GitHub repository** and deploy it.  
3. **Set the following environment variables** in Railway:  
   - `RAILWAY_PROJECT_ID`  
   - `RAILWAY_ENVIRONMENT_ID`  
   - `RAILWAY_SERVICE_ID`  
   - `RAILWAY_PUBLIC_DOMAIN`  
   - `API_TOKEN` (for authentication)  
4. **Start the service** and note the public domain.  

## **CI/CD Pipeline**  

### **Continuous Integration (CI)**  
- **Runs tests automatically** on pull requests using `pytest`.  
- **Fails** if any test fails.  

### **Continuous Deployment (CD)**  
- **Triggers on merging** to the `main` branch.  
- **Automatically deploys** the latest changes to Railway.  


## **API Endpoints**  

### **Retrieve a Book by ID**  
- **Endpoint:** `GET /api/v1/books/{book_id}`  
- **Response:**  
  - `200 OK` - Returns the book details 
  
   
  - `404 Not Found` - If the book does not exist  


```sh
{
  "id": 0,
  "title": "string",
  "author": "string",
  "publication_year": 0,
  "genre": "Science Fiction"
}

200 Ok
```

```sh
{
    "detail": "Book not found"
}

400  Not Found
```


## **Nginx Reverse Proxy Configuration**  
If deploying manually on a VPS, configure Nginx:

```sh
server {
    listen 80;
    server_name YOUR_DOMAIN;

    location / {
        proxy_pass http://127.0.0.1:8000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```