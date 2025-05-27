# EnviroDataHub Project

## Overview

This project is a backend service developed using Flask and PostgreSQL to create a REST API server with various features, including user management and device telemetry. Additionally, a device emulator application is created to send auto-generated environmental data to the server every minute.

## Features

- **Login API**
- **CRUD APIs for User Management**
- **CRUD APIs for Device Management**
- **API for getting time series data for a specific device**
- **API for getting the latest data for a specific device**
- **API for posting device telemetry**
- **Device Emulator to send data to the server every minute**

## Prerequisites

- Python 3.12
- PostgreSQL
- Flask
- Flask-SQLAlchemy
- Other dependencies listed in `requirements.txt`

## Installation

1. **Clone the repository**:
 
   git clone https://x-token-auth:ATCTT3xFfGN01SqjECM7YgtsvJSu0XOfSwUz7kGCX-eHb7imB23ZBgjMyrm-JnZGwXjFnJwNc_NLnv0HfqYe_uSWF59vz6R46r1dMSttQXTFYfYfdQElF-jYMZ5K1T97yoNZJav5Di1kc_MNNGsN0WG6wurvb2I3IwrW6JoUf8cDei8myFmJ6_4=DB518BA7@bitbucket.org/ngm_lab/summer-2024-training-backend.git

   cd summer-2024-training-backend


2. **Create a virtual environment**:
   
   python -m venv venv
  

3. **Activate the virtual environment**:
   - On Windows:
     
     venv\Scripts\activate
    
   - On macOS/Linux:
    
     source venv/bin/activate
    

4. **Install the dependencies**:
  
   pip install -r requirements.txt
   

## Database Setup

1. **Start PostgreSQL and create a database**:
   ```sql
   CREATE DATABASE summer_training_db;
   ```

2. **Configure the database URI in your Flask application**:
   Edit `config.py` to include your database credentials:
   ```python
   SQLALCHEMY_DATABASE_URI = 'postgresql://username:password@localhost/summer_training_db'
   ```

3. **Create database tables**:

   flask db init
   flask db migrate -m "Initial migration."
   flask db upgrade
 

## Running the Server

1. **Run the Flask application**:
  
   python app.py

   The server should now be running on `http://127.0.0.1:5000`.

## API Endpoints

- **Login API**: `POST /login`
- **User Management**:
  - `GET /users`
  - `POST /users`
  - `GET /users/<id>`
  - `PUT /users/<id>`
  - `DELETE /users/<id>`
- **Device Management**:
  - `GET /devices`
  - `POST /devices`
  - `GET /devices/<id>`
  - `PUT /devices/<id>`
  - `DELETE /devices/<id>`
- **Device Telemetry**:
  - `POST /devices/telemetry`
  - `GET /devices/<device_name>/timeseries`
  - `GET /devices/<device_name>/latest`

## Testing with Postman

1. **Open Postman** and create a new request.

2. **Set the request method and URL** according to the API endpoint you want to test.

3. **Set the Headers**:
   - For JSON payloads, add:
     ```http
     Content-Type: application/json
     ```

4. **Add Authorization Header** (for protected endpoints):
   - Obtain a JWT token from the login endpoint.
   - Add the header:
     ```http
     Authorization: Bearer <your_token>
     ```

5. **Set the Request Body** (for POST/PUT requests):
   - Select `raw` and `JSON` format.
   - Enter the JSON payload.

6. **Send the request** and check the response.

## Device Emulator

1. **Create a Python script `device_emulator.py`**:
   ```python
   import time
   import requests
   import json

   URL = "http://127.0.0.1:5000/devices/telemetry"
   DEVICE_NAME = "Device1"

   while True:
       data = {
           "device_name": DEVICE_NAME,
           "temperature": 22.5  # Replace with actual data generation logic
       }
       response = requests.post(URL, json=data)
       print(response.json())
       time.sleep(60)  # Send data every minute
   ```

2. **Run the device emulator**:
   
   python device_emulator.py
  

This README provides a comprehensive guide for setting up, running, and testing the Flask backend project.aining-backend
 
