# Overview
Project for todo app

## Structure

```bash
.
├── README.md
├── backend
│   ├── Dockerfile
│   ├── app.py
│   ├── entities
│   │   ├── __init__.py
│   │   ├── __pycache__
│   │   │   ├── __init__.cpython-39.pyc
│   │   │   └── task.cpython-39.pyc
│   │   └── task.py
│   └── requirements.txt
├── docker
│   └── dynamodb
├── docker-compose.yml
├── env.sample
└── frontend
    ├── Dockerfile
    ├── __pycache__
    │   └── app.cpython-39.pyc
    ├── app.py
    ├── requirements.txt
    └── templates
        ├── create.html
        ├── detail.html
        ├── index.html
        └── update.html

8 directories, 18 files
```

# Features
This app is able to use below function.

## User Story
- Add a task.
- Check detail of tasks.
- See the list of tasks.
- Delete tasks.
- Change status of task.
- Edit tasks.

# Using of language, framework, technology
- Python
- HTML/CSS
- Flask
- Docker compose
- DynamoDB
  
# Requirement
- Homebrew==3.3.4
- AWS CLI==2.3.3
- boto3==1.20.12
- Flask==2.0.2
- requests==2.26.0
- WTForms==3.0.0
 
# Installation
 
```bash
$ git clone https://github.com/hinatha/flask-on-docker.git
```

# Usage
 
```bash
$ docker-compose up
```
 
# Future plans
- Convert DB to RDBMS
