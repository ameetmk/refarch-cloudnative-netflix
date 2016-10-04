# IBM Cloud Architecture - Microservices Reference Application for Netflix OSS

Reference applications for deploying microservice-based applications onto IBM Bluemix, leveraging the Netflix OSS framework.

## Architecture

  ![Application Architecture](static/imgs/wfd-arch-v1.png?raw=true)

## Application Overview

The application is a simple dinner menu that displays available appetizers, entrees, and desserts for a non-existent restaurant.  There are several components of this architecture:

- Menu UI & Backend services aggregate all the options and display them to the user
- Individual microservices for menu options among Appetizers, Entrees, and Desserts
- Menu microservices communicate to each other using the [Netflix OSS Framework](https://netflix.github.io/):
    - [Zuul](https://github.com/Netflix/zuul) provides a proxy layer for the microservices.  
    - [Eureka](https://github.com/Netflix/eureka) provides a service registry.  The reusable Java Microservices register themselves to Eureka which allows clients to find them.

## Project Component Repositories

This project runs itself like a microservice project, as such each component in the architecture has its own Git Repository and tutorial listed below.  

Infrastructure Components:  

1. [Eureka](https://github.com/ibm-cloud-architecture/microservices-netflix-eureka)  - Contains the Eureka application components for microservices foundation  
2. [Zuul](https://github.com/ibm-cloud-architecture/microservices-netflix-zuul)  - Contains the Zuul application components for microservices foundation  

Application Components:  

1. [Menu UI](https://github.com/ibm-cloud-architecture/microservices-refapp-wfd-ui)  - User interface for presenting menu options externally  
2. [Menu Backend](https://github.com/ibm-cloud-architecture/microservices-refapp-wfd-menu)  - Exposes all the meal components as a single REST API endpoint, aggregating Appetizers, Entrees, and Desserts.  
3. [Appetizer Service](https://github.com/ibm-cloud-architecture/microservices-refapp-wfd-appetizer)  - Microservice providing a REST API for Appetizer options
4. [Entree Service](https://github.com/ibm-cloud-architecture/microservices-refapp-wfd-entree)  - Microservice providing a REST API for Entree options  
5. [Dessert Service](https://github.com/ibm-cloud-architecture/microservices-refapp-wfd-dessert)  - Microservice providing a REST API for Dessert options  

## Run the reference applications locally and in IBM Cloud

### Prerequisites: Environment Setup

- Install Java JDK 1.8 and ensure it is available in your PATH
- Install Docker on Windows or Mac

- Acquire the code
  - Clone the base repository:
    **`git clone https://github.com/ibm-cloud-architecture/microservices-netflix`**
  - Clone the peer repositories:
    **`./clonePeers.sh`**

### Run locally via Docker Compose

You can run the entire application locally on your laptop via Docker Compose, a container orchestration tool provided by Docker.

#### Step 1: Build locally

Run the following build script to build all the necessary Java projects.  This will build all the components required runnable JARs and package them into Docker containers.

  **`./build-all.sh`**

#### Step 2: Run Docker Compose

Run one of the following Docker Compose commands to start all the application components locally:

  - **`docker-compose up`** to run with output sent to the console _(for all 7 microservices)_  
    or  
  - **`docker-compose up -d`** to run in detached mode and run the containers in the backround.  

#### Step 3: Access the application

You can access the application after a few moments via **`http://localhost/whats-for-dinner`**!  That's easy enough!  

The backing services are automatically registered with Eureka and routed to the necessary dependent microservices, upon calling the _Menu_ service.

### Run on Bluemix via Cloud Foundry

Run the following script to deploy all the necessary Java projects as Cloud
Foundry apps.

  **`./deploy-to-cf.sh`**

### Run on Bluemix via IBM Container Service

**TBD End to End Setup**
