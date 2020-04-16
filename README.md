# policy-mgmt-service
[![License](http://img.shields.io/badge/license-APACHE-blue.svg?style=flat)](http://choosealicense.com/licenses/apache-2.0/)
[![SemVer](http://img.shields.io/badge/semver-2.0.0-blue.svg?style=flat)](http://semver.org/spec/v2.0.0)
[![Download](https://api.bintray.com/packages/cratekube/maven/policy-mgmt-service-client/images/download.svg)](https://bintray.com/cratekube/maven/policy-mgmt-service-client/_latestVersion)
[![Build Status](https://travis-ci.com/cratekube/policy-mgmt-service.svg?branch=master)](https://travis-ci.com/cratekube/policy-mgmt-service)
[![Coverage Status](https://coveralls.io/repos/github/cratekube/policy-mgmt-service/badge.svg?branch=master)](https://coveralls.io/github/cratekube/policy-mgmt-service?branch=master)

A service responsible for managing policies for kubernetes clusters

## Configuration
Internal and external services are configured by extending the Dropwizard application configuration with additional
settings. An environment variable parser is used to allow configuration settings to be overridden at runtime. 
These configuration options can be seen in the [app config file](app.yml).

## Local development

### Gradle builds
This project uses [gradle](https://github.com/gradle/gradle) for building and testing.  We also use the gradle wrapper
to avoid downloading a local distribution.  The commands below are helpful for building and testing.
- `./gradlew build` compile and build the application
- `./gradlew check` run static code analysis and test the application
- `./gradlew shadowJar` builds a fat jar that can be used to run the Dropwizard application

After you have generated the fat jar you can run your application with java using:
```bash
java -jar build/libs/policy-mgmt-service-1.0.0-SNAPSHOT-all.jar
```

### Docker builds
We strive to have our builds repeatable across development environments so we also provide a Docker build to generate 
the Dropwizard application container.  The examples below should be executed from the root of the project.

Running the base docker build:
```bash
docker build --target build .
```

Generating the Dropwizard application docker image:
```bash
docker build --target package -t policy-mgmt-service .
```

## Using the API client
This application generates a client for the Dropwizard application by using the swagger specification.  The maven asset
is available in JCenter, make sure you include the JCenter repository (https://jcenter.bintray.com/) when pulling this
client.  To use the client provide the following dependency in your project:

Gradle:
```groovy
implementation 'io.cratekube:policy-mgmt-service:1.0.0'
``` 

Maven:
```xml
<dependency>
  <groupId>io.cratekube</groupId>
  <artifactId>policy-mgmt-service</artifactId>
  <version>1.0.0</version>
</dependency>
```

## API Documentation
The API docs for this project are powered by the Swagger Specification. After starting up the application the available
APIs can be found at `http://localhost:<configured port>/swagger`

## Contributing
If you are interested in contributing to this project please review the [contribution guidelines](https://github.com/cratekube/cratekube/blob/master/CONTRIBUTING.md).
Thank you for your interest in CrateKube!
