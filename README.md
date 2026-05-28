# Expense Tracker Backend

## Overview

This is the backend service for the Expense Tracker application built using FastAPI and MySQL.

The backend provides REST APIs for:

- Add Expense
- View Expenses
- Update Expense
- Delete Expense
- Search Expenses
- Sort Expenses

The backend is deployed on Render and connected to Aiven MySQL cloud database.

---

# Backend Repository

https://github.com/bhargaviraniganta/expense_tracker_be

---

# Tech Stack

- Python
- FastAPI
- MySQL
- Aiven Cloud Database
- Render Deployment
- Pydantic
- Uvicorn

---

# Project Structure

```bash
expense_tracker_be/
│
├── main.py
├── database.py
├── requirements.txt
├── .env
└── README.md
```

---

# Installation

## Clone Repository

```bash
git clone https://github.com/bhargaviraniganta/expense_tracker_be.git
```

## Navigate to Project Folder

```bash
cd expense_tracker_be
```

## Install Dependencies

```bash
pip install -r requirements.txt
```

---

# requirements.txt

```txt
fastapi
uvicorn
mysql-connector-python
python-dotenv
pydantic
```

---

# Create .env File

```env
HOST=your_host
USER=avnadmin
PASSWORD=your_password
DATABASE=defaultdb
PORT=12345
```

---

# Run Application

```bash
uvicorn main:app --reload
```

Backend runs on:

```text
https://expense-tracker-be-1n3i.onrender.com
```

---

# API Documentation

FastAPI automatically provides Swagger UI.

Open:

```text
http://127.0.0.1:8000/docs
```

---

# Database Table

```sql
CREATE TABLE expenses(

expense_id INT AUTO_INCREMENT PRIMARY KEY,

title VARCHAR(100),

amount FLOAT,

category VARCHAR(50),

created_at TIMESTAMP
DEFAULT CURRENT_TIMESTAMP

);
```

---

# Database Connection

## database.py

```python
import mysql.connector
import os

from dotenv import load_dotenv

load_dotenv()

def get_connection():

    connection=mysql.connector.connect(

        host=os.getenv("HOST"),

        user=os.getenv("USER"),

        password=os.getenv("PASSWORD"),

        database=os.getenv("DATABASE"),

        port=os.getenv("PORT")

    )

    return connection
```

---

# CORS Configuration

CORS is required because:

- Frontend runs on Streamlit Cloud
- Backend runs on Render

Add inside `main.py`

```python
from fastapi.middleware.cors import CORSMiddleware
```

```python
origins=[

    "http://localhost:8501",

    "https://your-streamlit-app.streamlit.app"

]

app.add_middleware(

    CORSMiddleware,

    allow_origins=origins,

    allow_credentials=True,

    allow_methods=["*"],

    allow_headers=["*"]

)
```

---

# API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | / | Home API |
| POST | /expenses | Add Expense |
| GET | /expenses | Get All Expenses |
| GET | /expenses/{id} | Get Single Expense |
| PUT | /expenses/{id} | Update Expense |
| DELETE | /expenses/{id} | Delete Expense |
| GET | /search?category=Food | Search Expenses |
| GET | /sort?sort_by=price_desc | Sort Expenses |

---

# API Features

## Add Expense

Adds a new expense into MySQL database.

Uses:

- POST API
- JSON Payload
- INSERT Query

---

## View Expenses

Fetches all expenses from database.

Uses:

- GET API
- SELECT Query

---

## Update Expense

Updates existing expense using Expense ID.

Uses:

- PUT API
- Path Parameters
- UPDATE Query

---

## Delete Expense

Deletes expense using Expense ID.

Uses:

- DELETE API
- DELETE Query

---

## Search Expense

Filters expenses by category.

Example:

```text
/search?category=Food
```

Uses:

- Query Parameters
- WHERE Clause

---

## Sort Expense

Sorts expenses by:

- Latest Date
- Oldest Date
- Highest Price
- Lowest Price

Uses:

- ORDER BY
- Query Parameters

---

# HTTP Methods Used

| Method | Purpose |
|---|---|
| GET | Fetch Data |
| POST | Insert Data |
| PUT | Update Data |
| DELETE | Remove Data |

---

# Status Codes

| Status Code | Meaning |
|---|---|
| 200 | Success |
| 404 | Expense Not Found |
| 422 | Validation Error |
| 500 | Internal Server Error |

---

# Deployment

## Backend Deployment Platform

Render

---

# Render Deployment Steps

1. Push backend code to GitHub
2. Open Render Dashboard
3. Create New Web Service
4. Connect GitHub Repository
5. Add Environment Variables
6. Deploy Application

---

# Render Start Command

```bash
uvicorn main:app --host 0.0.0.0 --port $PORT
```

---

# Environment Variables in Render

Add these variables inside Render dashboard:

- HOST
- USER
- PASSWORD
- DATABASE
- PORT

---

# Cloud Database

Database hosted using Aiven MySQL Cloud.

Advantages:

- Cloud Hosting
- Remote Access
- Secure Connections
- Easy Deployment Integration

---

# Concepts Used

## Backend Concepts

- FastAPI
- REST APIs
- CRUD Operations
- JSON Responses
- Path Parameters
- Query Parameters
- Status Codes

## Database Concepts

- INSERT
- SELECT
- UPDATE
- DELETE
- WHERE
- ORDER BY

## Deployment Concepts

- Render Deployment
- Environment Variables
- Cloud Database Integration
- CORS Policy

---

# Future Improvements

- JWT Authentication
- User Login System
- Expense Analytics APIs
- Export CSV APIs
- Pagination
- Monthly Reports

---

# Author

Bhargavi Rani Ganta
