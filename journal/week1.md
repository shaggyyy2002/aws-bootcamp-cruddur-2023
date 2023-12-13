# Week 1 — App Containerization

## What is Containerization?

Containerization is a software deployment process that bundles an application’s code with all the files and libraries it needs to run on any infrastructure. 

Traditionally, to run any application on your computer, you had to install the version that matched your machine’s operating system. 

For example, you needed to install the Windows version of a software package on a Windows machine. However, with containerization, you can create a single software package, or container, that runs on all types of devices and operating systems. 

## What are the benefits of containerization?

Developers use containerization to build and deploy modern applications because of the following advantages:

**Portability:** Software developers use containerization to deploy applications in multiple environments without rewriting the program code.They build an application once and deploy it on multiple operating systems. For example, they run the same containers on Linux and Windows operating systems. Developers also upgrade legacy application code to modern versions using containers for deployment.

**Scalability:** Containers are lightweight software components that run efficiently. For example, a virtual machine can launch a containerized application faster because it doesn't need to boot an operating system. Therefore, software developers can easily add multiple containers for different applications on a single machine. The container cluster uses computing resources from the same shared operating system, but one container doesn't interfere with the operation of other containers.  

**Fault tolerance:** Software development teams use containers to build fault-tolerant applications. They use multiple containers to run microservices on the cloud. Because containerized microservices operate in isolated user spaces, a single faulty container doesn't affect the other containers. This increases the resilience and availability of the application.

**Agility:** Containerized applications run in isolated computing environments. Software developers can troubleshoot and change the application code without interfering with the operating system, hardware, or other application services. They can shorten software release cycles and work on updates quickly with the container model.

## What is DockerHub?

[DockerHub](https://hub.docker.com/) is a container registry built for developers and open source contributors to find, use, and share their container images. With Hub, developers can host public repos that can be used for free, or private repos for teams and enterprises.

> You could say that Dockerhub is Github but for container images.

## Dockerfile

Docker can build images automatically by reading the instructions from a Dockerfile. A Dockerfile is a text document that contains all the commands a user could call on the command line to assemble an image.

In our case we have used seprate Dockerfile for Frontend & Backend.

*`Frontend Dockerfile:`*

```Dockerfile
FROM node:16.18

ENV PORT=3000

COPY . /frontend-react-js

WORKDIR /frontend-react-js

RUN npm install

EXPOSE ${PORT}

CMD ["npm", "start"]
```

*`Backend Dockerfile:`*

```Dockerfile
# Base Image for Python:version
FROM python:3.10-slim-buster

# This will create our workdir and cd into it
WORKDIR /backend-flask

# Copies our file from our source to destination path
COPY requirements.txt requirements.txt

# The RUN instruction will execute any commands in a new layer on top of the current image and commit the results
RUN pip3 install -r requirements.txt

COPY . .

# The ENV instruction sets the environment variable <key> to the value <value>. 
# This value will be in the environment for all subsequent instructions in the build stage and can be replaced inline in many as well.
ENV FLASK_ENV=development

EXPOSE ${PORT}

# CMD (Command)
# python3 -m flask run --host=0.0.0.0 --port=4567
CMD [ "python3", "-m" , "flask", "run", "--host=0.0.0.0", "--port=4567"]
```

## Run Dockerfile

To run our Dockerfile we will have to build our image and run it using Docker Commands.

To Build the Dockerfile. Locate to where your Dockerfile is present. 

*`For frontend:`*
```sh
cd frontend-react-js
docker build -t <dockerhub-username>/aws-cruddur-frontend:<version> .
```

*`For backend:`*
```sh
cd backend-flask
docker build -t <dockerhub-username>/aws-cruddur-backend:<version>
```

## Push Images to DockerHub

To push DockerImages to Dockerhub login to dockerhub using CLI. 

```
docker login
```
 Once logged in we now want to push our DockerImage to the Repository. 

*`For frontend:`*
```sh
docker push <dockerhub-username>/aws-cruddur-frontend:<version>
```

*`For backend:`*
```sh
docker push <dockerhub-username>/aws-cruddur-backend:<version>
```

> *find all the commands: [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/).*

## Docker Compose

Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. Then, with a single command, you create and start all the services from your configuration.

Compose works in all environments; production, staging, development, testing, as well as CI workflows. It also has commands for managing the whole lifecycle of your application:


1. *Start, stop, and rebuild services.*
2. *View the status of running services.*
3. *Stream the log output of running services.*
4. *Run a one-off command on a service.*

```yaml
version: "3.8"
services:
  backend-flask:
    image: nitin03/aws-cruddur-backend:v1.0.0
    ports:
      - "4567:4567"
    environment:
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      OTEL_SERVICE_NAME: 'backend-flask'
      OTEL_EXPORTER_OTLP_ENDPOINT: "https://api.honeycomb.io"
      OTEL_EXPORTER_OTLP_HEADERS: "x-honeycomb-team=${HONEYCOMB_API_KEY}"
    volumes:
      - ./backend-flask:/backend-flask
  frontend-react-js:
    environment:
      REACT_APP_BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      FRONTEND_URL: "https://3000-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
      BACKEND_URL: "https://4567-${GITPOD_WORKSPACE_ID}.${GITPOD_WORKSPACE_CLUSTER_HOST}"
    image: nitin03/aws-cruddur-frontend:v1.0.0
    ports:
      - "3000:3000"
    volumes:
      - ./frontend-react-js:/frontend-react-js

# the name flag is a hack to change the default prepend folder
# name when outputting the image names
networks: 
  internal-network:
    driver: bridge
    name: cruddur
```

To start the docker-compose.yml file use: 

```sh
docker-compose up
```

To stop use:

```sh
docker-compose down
```

## Add PostgresSQL & DynamoDB to Dockercompose file

### Postgres

```yaml
services:
  db:
    image: postgres:13-alpine
    restart: always
    environment:
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=password
    ports:
      - '5432:5432'
    volumes: 
      - db:/var/lib/postgresql/data
volumes:
  db:
    driver: local
```

To install the postgres client into Gitpod

```sh
  - name: postgres
    init: |
      curl -fsSL https://www.postgresql.org/media/keys/ACCC4CF8.asc|sudo gpg --dearmor -o /etc/apt/trusted.gpg.d/postgresql.gpg
      echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
      sudo apt update
      sudo apt install -y postgresql-client-13 libpq-dev
```
### DynamoDB Local

```yaml
services:
  dynamodb-local:
    # https://stackoverflow.com/questions/67533058/persist-local-dynamodb-data-in-volumes-lack-permission-unable-to-open-databa
    # We needed to add user:root to get this working.
    user: root
    command: "-jar DynamoDBLocal.jar -sharedDb -dbPath ./data"
    image: "amazon/dynamodb-local:latest"
    container_name: dynamodb-local
    ports:
      - "8000:8000"
    volumes:
      - "./docker/dynamodb:/home/dynamodblocal/data"
    working_dir: /home/dynamodblocal
```

Example of using DynamoDB local
https://github.com/100DaysOfCloud/challenge-dynamodb-local

## Volumes

directory volume mapping

```yaml
volumes: 
- "./docker/dynamodb:/home/dynamodblocal/data"
```

named volume mapping

```yaml
volumes: 
  - db:/var/lib/postgresql/data

volumes:
  db:
    driver: local
```

## Container Security Best Practices

Now that we have learned about containerization it would not be secure if anyone could change or acess our container isnt'it? 

Container security involves defining and adhering to build, deployment, and runtime practices that protect a Linux container—from the applications they support to the infrastructure they rely on.

1. Keep host & Docker to latest security patches.
2. Docker daemon & containers should run in non-root user mode.
3. Image Vulnerability Scanning.
4. Trusting a Private Vs Public Image Registry.
5. No Sensetive data in Dockerfile or DockerImages
6. Use Secret management services to share secrets.
7. Read only filesystems & Volumes in Docker.
8. Seprate Databases for long term storage.
9. Use DevSecOps practises while building application security.
10. Ensure all code is tested for vulnerabilites before production use.

## **Resources:** 

- [What is Containerization?](https://aws.amazon.com/what-is/containerization/)
- [Docker Images by LinuxServer](https://docs.linuxserver.io/images/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [DynamoDB dockercompose](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DynamoDBLocal.DownloadingAndRunning.html) 
- [Setup Health Check in Docker Compose](https://www.paulsblog.dev/how-to-successfully-implement-a-healthcheck-in-docker-compose/)

## **Tips/Best Practices**

- To improve the quailty of your docker-compose file and dockerfile you can check various open source org's Dockerfile & docker-compose file. 