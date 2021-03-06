# DSA Assignment 3

## Assignment prerequisites
1. [Python 3.8](https://www.python.org/downloads/)
2. [mySQl 8.0](https://dev.mysql.com/downloads/installer/)
3. [postman][https://www.postman.com/downloads/]

 if computer support docker and kubernetes (Optional)
4. [Docker][https://docs.docker.com/desktop/windows/install/]
5. [kubernetes][https://kubernetes.io/docs/tasks/tools/install-kubectl-windows/]
6. [minikube][https://minikube.sigs.k8s.io/docs/start/]


## Kafka Setup (Run kafka zookeeper and server)
1. .\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties
2. .\bin\windows\kafka-server-start.bat .\config\server.properties 
3. .\bin\windows\connect-distributed.bat config/connect-distributed.properties

## Run HoD and Lecture

### Leacture create course outline
method: POST
url: localhost:9096/courseOutline/Leacture/createCourseOutline
JSON body: 
    {
        "courseInformation": {
            "Code": "DSA621S",
            "Title": "Distributed Systems and Applications",
            "Programme": "07BACS, Computer Science (Software Development)",
            "Department": "Computer Science",
            "ContactHours": "120 hours",
            "CourseFormat": "45 hours face?to?face contact with the lecturer, 42 hours directed self?learning and self?directed learning, 15 hours supervised tutorial, 18 hours assessment",
            "EffectiveDate": "2021-09-14 23:18:17",
            "PreRequisites": "Programming 2 (P RG620S)",
            "CourseDescription": "The aim of this course is to introduce the students to the principles and concepts of distributed systems, protocols and interfaces.",
            "NQFLevelAndCredit": "NQF Level 6, credits: 12",
            "CourseEquivalences": "Object?Oriented Programming (OOP521S)",
            "CourseDeliveryMethods": "The delivery of the course is by theory and practical.The practical will be based on a student?centeredapproach. It will also involve a group of studentscarrying out a group project."
        },
        "LeactureInformation": [
            {
                "Name": "Jos G. Quenum",
                "Email": "jquenum@nust.na",
                "OfficeHours": "08:00  16:30",
                "OfficePhone": "207 2235",
                "OfficeLocation": "Lower Campus, Science & Technology Bld.",
                "ConsultationHours": "Wednesdays (10:30  12:30)"
            },
            {
                "Name": "Lameck Amugongo",
                "Email": "lamugongo@nust.na",
                "OfficeHours": "08:00  16:30",
                "OfficePhone": "207 2234",
                "OfficeLocation": "Lower Campus, Science & Technology Bld.",
                "ConsultationHours": "Wednesdays (10:30  12:30)"
            }
        ],
        "LearningOutcomes": [
            "Analyze the principles and mechanisms used in Distributed Systems;",
            "Demonstrate knowledge of the current technologies and their application;",
            "Design and develop distributed applications."
        ],
        "CourseContent": [
            "Distributed Systems and their characteristics",
            "Applications: Service?oriented Computing",
            "Communication: (Inter?process Communication,Remote Invocation, Indirect Communication, API design and Implementation)",
            "More Applications (Distributed Data Stores, Security & Fault Tolerance)",
            "Distributed Algorithms (Logical Time & Global State, Coordination & Consensus, Transactions and concurrency models)"
        ],
        "IsSignedByLeacture": false,
        "IsApprovedByHoD": false
    }

### Lecture view create Course outline
method: GET
url: localhost:9096/courseOutline/Leacture/viewCourseOutlines?Id=1

### Leacture Sign Course Outline
method: PUT
url: localhost:9096/courseOutline/Leacture/signCourseOutline?Id=1

### HoD View course Outline
method: GET
url: localhost:9097/courseOutline/HoD/viewCourseOutlines

### HoD approves the course outline
method: PUT
url: localhost:9097/courseOutline/HoD/approveCourseOutline?Id=1

## Setup debezium

### Create debezium Connector
method: PUT
url: http://localhost:8083/connectors/
JSON body: {
      "name": "mysql-connector",
      "config": {
            "connector.class": "io.debezium.connector.mysql.MySqlConnector",
            "database.hostname": "localhost",
            "database.port": "3306",
            "database.user": "root",
            "database.password": "@Thom-lax11",
            "database.server.id": "42",
            "database.server.name": "computingandinformatics",
            "database.history.kafka.bootstrap.servers": "localhost:9092",
            "database.history.kafka.topic": "dbhistory.demo" ,
            "include.schema.changes": "true"
       }
    }

### Verify debezium Connector
method: GET
url: http://localhost:8083/connectors/mysql-connector/status


## Run Client


## Deploy to kubernetes
1. Start minikube
2. minikube -p minikube docker-env | Invoke-Expression#   D S A  
 