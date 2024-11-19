# Easy setup of the whole environment

The Setup is part of the CMC Knowledge Graph Application.
This repository helps settings up a local environment based on Docker Compose.

## Installation instructions

1. Install Docker Desktop for Windows from [Docker Hub](https://hub.docker.com/editions/community/docker-ce-desktop-windows/) (latest test with Docker Desktop v2.2.0.3)
2. Clone this repository locally
    ```console
    git clone --recursive [URL to this Git repo]
    ```
3. Pull all changes in all submodules
    ```console
    git pull --recurse-submodules
    ```
4. Create a file `.env` in parallel to the file `docker-compose.yml` and insert the following variables (example values are shown):
    ```
    GRAPHDATABASE_USERNAME=admin
    GRAPHDATABASE_PASSWORD=admin
    ```
5. Run `docker-compose up` to download and build all Docker images and startup the environment
6. Wait for docker-compose to start up
7. Open the KGE Frontend (see URL below). 
****

### Known problems

- While building the frontend the following error could occur. In the Dockerfiles of the frontend applications node is used with an increased heap size while building the applications `node --max_old_space_size=8000`. Try to increase this, if the error occurs.
    ```
    FATAL ERROR: Ineffective mark-compacts near heap limit Allocation failed - JavaScript heap out of memory
    ```
- After starting the application a second time, the fuseki database could throw exceptions. Delete the Docker container of the fuseki database with `docker container rm fuseki`. ATTENTION: This will remove all your created data and reload the database with the initial data.

- fuseki-loader/loader.sh could contain `Carriage Return` characters, remove them.

## Application URLs

| Component                                                | URL for Docker environment      | URL for local environment       | Username | Password |
| -------------------------------------------------------- | ------------------------------- | ------------------------------- |--------- | -------- |
| Apache Jena Fuseki Database Webinterface                 | http://localhost:3030/          | -                               | admin    | admin    |
| KGE-Editor-Frontend                         | http://localhost:4400/ | http://localhost:4400/| -        | -        |
| KGE-Web-Service                         | http://localhost:8080/swagger | http://localhost:8080/swagger| -        | -        |
## Quick Tips

Some quick tips and advices to work faster.

### Docker

To purge all unused or dangling images, containers, volumes, and networks run the following command:
```console
docker system prune -a
```

To remove all containers:
```console
docker container rm $(docker container ls -aq)
```


### Links

- [Git Submodules](https://www.vogella.com/tutorials/GitSubmodules/article.html)
- [Markdown Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)
- [Apache Jena Fuseki tdbloader example](https://www.csee.umbc.edu/courses/graduate/691/spring14/01/examples/jena/README.txt)