# Step 2 - FrontEnd team adding Docker Support

FrontEnd team is responsible for a small part of the whole solution build by the company. Others teams will build services that might be, direct or indirectly, dependents on their services.

They needed a place to deploy their applications with security, isolation, rolling updates, networking, capable of running multiple stacks (they wish to migrate their web FrontEnd to Angular in the future).

Containers allows them to isolate an application piece (web or api in their case) in a standard way so that can executed by different hosts and operation systems. Using virtual machines would require them to install the required frameworks on the host for each version used. Containers allows them to build the dependency directly into the image that will be used to run the application. It allows a Linux OS without NodeJS, .NET Core and Java installed to execute code written in any of these programming stacks.

## Container Developer Experience

For the FrontEnd team it is important to continue to have the rich experience provided by Visual Studio, allowing the to debug their code without cerimonies.

Visual Studio tooling makes it easy to start working with Docker. For instance to add Docker support to the FrontEnd solution right click on each project and select Add &rarr; Container Orchestrator Support.

This will create a Dockerfile with instructions on how to build the docker image. It will also create a docker-compose project that allows debugging multiple containers inside Visual Studio.

The docker compose file defines how each project is built and their dependencies (web depends on the api):

```yaml
version: '3.4'

services:
  frontend-api:
    image: ${DOCKER_REGISTRY}frontendapi
    build:
      context: .
      dockerfile: src/FrontEnd.Api/Dockerfile

  frontend-web:
    image: ${DOCKER_REGISTRY}frontendweb
    build:
      context: .
      dockerfile: src/FrontEnd.Web/Dockerfile
    depends_on:
      - frontend-api
```

Running the docker-compose project will allows the team to debug both projects. Docker compose also allows calling the api with the internal address of http://frontend-api, since this is how we defined the service name.

The Frontend team now is able to create container images from Visual Studio. The development experience is still as before, allowing them to easily debug their code.

In the next step we will look into how they can bring their application to production.

 
[Go to Start](./ReadMe.md)\
[Go to previous step](./Step1.md)\
[Go to next step](./Step3.md)