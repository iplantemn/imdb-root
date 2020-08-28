# imdb-root
Root project for the IMDB SmartThings project.

**Author**: Isabelle Plante
* **Github**: https://github.com/iplantemn
* **LinkedIn**: https://www.linkedin.com/in/isabelleplante
* **Email**: iplante@me.com

## Dependencies

These Github subprojects are necessary to run the entire project:

| Project           | Github URL |
| :---------------- | :--- |
| `imdb-cast-api`   | https://github.com/iplantemn/imdb-cast-api   |
| `imdb-movies-api` | https://github.com/iplantemn/imdb-movies-api |

It is assumed that you will clone these projects in this directory.

## Documentation
### Databases

This project contains two MySQL database, deployed to Docker. I'm sharing the password because these applications and
 databases are not deployed to any live environment and are used locally only.

| Subproject | Connection string           | Schema | Username | Password               |
| :--------- | :-------------------------- | :----- | :------- | :--------------------- |
| cast       | jdbc:mysql://localhost:3307 | cast   | cast     | `3vxoYADFrhW3iNAG8VxT` |
| movies     | jdbc:mysql://localhost:3308 | movies | movies   | `fEvfvJz8mKfjkV943JTA` |

### APIs

Each database has a API exposing endpoints to perform all CRUD operations. These can be deployed to Docker or locally.

| Subproject | Hostname (Docker)            | API             |
| :--------- | :--------------------------- | --------------- |
| cast       | localhost:5013/cast-api      | `api/v1/cast`   |
| movies     | localhost:5012/movies-api    | `api/v1/movies` |


## Deploying databases and services

### Prerequisite

You must have Docker installed and running.

### 1. Create network

```
docker network create imdb
```

### 2. Deploy databases

```shell script
# Cast database
cd imdb-cast-api
docker-compose up cast-db
cd ..

# Movies database
cd imdb-movies-api
docker-compose up movies-db
cd ..
```

### 3. Build & deploy applications

**Warning**: These applications rely on the databases being up and running.\
**Note**: If you're using Windows, replace `./gradlew` with `gradlew`. Note that this project was fully developed and tested using macOS.

```shell script
# Cast application
cd imdb-cast-api
./gradlew build && docker-compose up cast-api
cd ..

# Movies application
cd imdb-movies-api
./gradlew build && docker-compose up movies-api
cd ..
```

## TODO
1. PMD
1. Write tests
1. Swagger