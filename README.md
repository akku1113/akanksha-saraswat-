# akanksha-saraswat-
Test for Backend Role 

# Secure File Sharing System

## Overview
This is a secure file-sharing system that allows Operations Users (Ops User) to upload specific file types and Client Users to sign up, verify their email, login, list uploaded files, and download files securely.

## Technologies Used
- Python
- Flask (Web Framework)
- SQLAlchemy (SQL Database)
- Flask JWT Extended (JSON Web Tokens for Authentication)

## Installation
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/secure-file-sharing-system.git
# Install dependencies:
pip install -r requirements.txt
# Run the application:
python app.py

## To implement a secure file-sharing system between two types of users (Ops User and Client User) using Python, a REST API, and a SQL database, you can use the Flask framework for building the API and SQL Alchemy for database interactions. Here's a basic outline of how you can structure the code:
# Install Required Packages:
pip install flask flask_sqlalchemy flask_jwt_extended

# Create the Flask Application:
from flask import Flask, request, jsonify
from flask_sqlalchemy import SQLAlchemy
from flask_jwt_extended import JWTManager, create_access_token, jwt_required, get_jwt_identity

app = Flask(__name__)
app.config['SQLALCHEMY_DATABASE_URI'] = 'sqlite:///file_share.db'
app.config['SQLALCHEMY_TRACK_MODIFICATIONS'] = False
app.config['JWT_SECRET_KEY'] = 'your-secret-key'
jwt = JWTManager(app)
db = SQLAlchemy(app)

# Create Database Models:
class User(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    username = db.Column(db.String(50), unique=True, nullable=False)
    email = db.Column(db.String(120), unique=True, nullable=False)
    password = db.Column(db.String(120), nullable=False)
    is_ops_user = db.Column(db.Boolean, default=False)

class File(db.Model):
    id = db.Column(db.Integer, primary_key=True)
    filename = db.Column(db.String(255), nullable=False)
    user_id = db.Column(db.Integer, db.ForeignKey('user.id'), nullable=False)

# Create Endpoints for Ops User:
@app.route('/ops/login', methods=['POST'])
def ops_login():
    # Implement login logic for Ops User

@app.route('/ops/upload', methods=['POST'])
@jwt_required()
def ops_upload():
    # Implement file upload logic for Ops User

# Create Endpoints for Client User:
@app.route('/client/signup', methods=['POST'])
def client_signup():
    # Implement signup logic for Client User

@app.route('/client/verify/<token>', methods=['GET'])
def client_verify(token):
    # Implement email verification logic for Client User

@app.route('/client/login', methods=['POST'])
def client_login():
    # Implement login logic for Client User

@app.route('/client/files', methods=['GET'])
@jwt_required()
def client_list_files():
    # Implement logic to list all uploaded files for Client User

@app.route('/client/download/<file_id>', methods=['GET'])
@jwt_required()
def client_download_file(file_id):
    # Implement logic to generate a secure, expiring download URL for Client User

# Run the Application:
if __name__ == '__main__':
    db.create_all()
    app.run(debug=True)



