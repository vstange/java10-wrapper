# java10-wrapper test

## Prerequisite

- Open JDK 10
  - Download Open JDK 10 from https://adoptopenjdk.net
  - Extract *.tar.gz into persistent directory
  - Setup it as a SDK in your IDE
  
- Docker
  - Download and install Docker from https://docs.docker.com/install/

## Initialization

- Checkout repository via git
- Import repository in IntelliJ IDEA
- Click `File > Open` and select repository's folder
- Let IntelliJ do its magic to resolve Maven modules

## Build

The Docker build is dependent on the target files build by the Maven build process.
Maven must run for before Docker.

### Maven

    mvn clean install

### Docker

    docker build -t java10wrapper .

   
Test if docker runs fine

    docker run --rm -it java10wrapper java -version
    
and test the AION API Demo
    
    docker run --rm -it java10wrapper java -jar java-wrapper.jar -h

## AION API

https://mvnrepository.com/artifact/org.aion.network/aion_api

GitHub Page: https://github.com/aionnetwork/aion_api

    # How the submodule was added
    git submodule add -b master git@github.com:aionnetwork/aion_api.git
    git submodule init 
    
    # Update submodule (submodule --remote fetches new commits in the submodules)
    git submodule update --remote

Build documentation: https://github.com/aionnetwork/aion_api/wiki/Api-Build-Guild

    cd aion_api
    ./gradlew clean
    ./gradlew build

Had to change in the `gradlew` file: 
`JAVACMD` replaced with `/home/vstange/jdk/jdk-10.0.2+13/bin/java` my 
local Java 10 call, since my JAVA_HOME targets my Java 8 installation.

**Jar** can be found in `./pack`

# Test Data

## Docker Images Sizes

| ID | Version | Size
| ------------ | ------ | -------
| adoptopenjdk/openjdk10 | alpine | 781 MB 

