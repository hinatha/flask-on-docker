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

## Create table
```bash
H.Kondo@HK-MacBook-Air flask-on-docker % docker ps
CONTAINER ID   IMAGE                          COMMAND                  CREATED          STATUS          PORTS                    NAMES
65df63f8ce14   flask-on-docker_backend        "python app.py"          17 minutes ago   Up 17 minutes   0.0.0.0:5001->5001/tcp   backend
4b494ec88453   amazon/dynamodb-local:latest   "java -jar DynamoDBL…"   17 minutes ago   Up 17 minutes   0.0.0.0:8000->8000/tcp   dynamodb-local
5a807521013d   flask-on-docker_frontend       "python app.py"          17 minutes ago   Up 17 minutes   0.0.0.0:8080->8080/tcp   frontend
H.Kondo@HK-MacBook-Air flask-on-docker % aws dynamodb list-tables --endpoint-url http://localhost:8000
{
    "TableNames": []
}
H.Kondo@HK-MacBook-Air flask-on-docker % aws dynamodb create-table \
> --table-name dev-tasks \
> --attribute-definitions AttributeName=task_id,AttributeType=S \
> --key-schema AttributeName=task_id,KeyType=HASH \
> --provisioned-throughput ReadCapacityUnits=1,WriteCapacityUnits=1 \
> --endpoint-url http://localhost:8000
{
    "TableDescription": {
        "AttributeDefinitions": [
            {
                "AttributeName": "task_id",
                "AttributeType": "S"
            }
        ],
        "TableName": "dev-tasks",
        "KeySchema": [
            {
                "AttributeName": "task_id",
                "KeyType": "HASH"
            }
        ],
        "TableStatus": "ACTIVE",
        "CreationDateTime": "2022-01-03T16:43:10.391000+09:00",
        "ProvisionedThroughput": {
            "LastIncreaseDateTime": "1970-01-01T09:00:00+09:00",
            "LastDecreaseDateTime": "1970-01-01T09:00:00+09:00",
            "NumberOfDecreasesToday": 0,
            "ReadCapacityUnits": 1,
            "WriteCapacityUnits": 1
        },
        "TableSizeBytes": 0,
        "ItemCount": 0,
        "TableArn": "arn:aws:dynamodb:ddblocal:000000000000:table/dev-tasks"
    }
}
H.Kondo@HK-MacBook-Air flask-on-docker % aws dynamodb list-tables --endpoint-url http://localhost:8000
{
    "TableNames": [
        "dev-tasks"
    ]
}
H.Kondo@HK-MacBook-Air flask-on-docker % docker-compose exec backend /bin/ash
/src # apk add bind-tools
(1/7) Installing fstrm (0.6.1-r0)
(2/7) Installing json-c (0.15-r1)
(3/7) Installing protobuf-c (1.4.0-r0)
(4/7) Installing libuv (1.42.0-r0)
(5/7) Installing libxml2 (2.9.12-r2)
(6/7) Installing bind-libs (9.16.22-r4)
(7/7) Installing bind-tools (9.16.22-r4)
Executing busybox-1.34.1-r3.trigger
OK: 21 MiB in 47 packages
/src # nslookup dynamodb-local
Server:         127.0.0.11
Address:        127.0.0.11#53

Non-authoritative answer:
Name:   dynamodb-local
Address: 172.28.0.3

/src # dig dynamodb-local

; <<>> DiG 9.16.22 <<>> dynamodb-local
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 26437
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;dynamodb-local.                        IN      A

;; ANSWER SECTION:
dynamodb-local.         600     IN      A       172.28.0.3

;; Query time: 4 msec
;; SERVER: 127.0.0.11#53(127.0.0.11)
;; WHEN: Mon Jan 03 07:44:39 UTC 2022
;; MSG SIZE  rcvd: 62

/src # apk add curl 
OK: 21 MiB in 47 packages
/src # curl http://0.0.0.0:5001/tasks
[]
/src # exit
```
 
# Future plans
- Convert DB to RDBMS
