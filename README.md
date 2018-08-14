# Containers on Azure

## The application

Bank application, covering multiple scenarios where we can demonstrate:

- Container development experience with Azure, Visual Studio Code and Visual Studio
- Microservices deployment
- Microservice security (authentication/authorization)
- Microservice architecture fundamentals
  - Eventual consistence
  - Messaging/Queuing
- Scalability (auto-scale)
- Collaboration between teams (Team1 using Team2 microservices)

## How to document the solution

Having a set of branches that solve a simple problem. For instance:

- Branch 00: Initial commit
- Branch 01: Added docker support
- Branch 02: Added CI/CD
- Branch 03: Added integration tests
- Branch 99: ...

## The Microservices

Simulate multiple teams working of complete solution. Each team has it’s own repository.

|Team|Responsible for|Tech Stack|
|-|-|-|
|Team1|Banking Web Frontend|Razor Pages, Angular|
|Team2|User Management|ASP.NET Core, NodeJS|
|Team3|Stock Management|ASP.NET Core, NodeJS|
|Team4|Account Transactions|ASP.NET Core, NodeJS|

## Use cases

- Banking login
  - IdentityServer, AD B2C, OpenIdDict
- Portfolio management
  - View
  - Sell
  - Buy
  - Recommendations
- Account overview


## The Orchestrators

How the distinct orchestrators compare to each other?

- AKS
  - Virtual Kubelet – ACI
  - Setting up with Terraform, ARM, cli, Portal
- OpenShift on Azure
- Managed OpenShift (N/a atm)
- Service Fabric Mesh

## The Development Experience

How is the development experience using Microsoft/OSS solutions?

- Different languages: C#, NodeJS, Java, Go
- Development Productivity: DevSpaces

## Developing Microservices

Coding/patterns writing  Microservices in C#

- DDD7
- Mediatr
- Simple CRUD

## DevOps

Play around with the different DevOps/Container tools available

### CI/CD

- Using VSTS
  - Build agents in cluster
- Using Jenkins
- Git based deployment
- Using Helm charts
- Versioning
- Using KeyVault for secrets (connection strings, hashs, etc.)
- Unit Tests & Integration Tests

### TLS/SSL

### Ingress

- Envoy
- Nginx

### Service Mesh

- Istio
- Envoy
- References:
  - [https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc](https://blog.envoyproxy.io/service-mesh-data-plane-vs-control-plane-2774e720f7fc)

### Application Monitoring

- Application Insights
- Prometheus

### Scalability tests

- Demonstrate auto-scale working

## Steps

- [Step 1 - FrontEnd team Kick-off](./Step1.md)
- [Step 2 - FrontEnd team adding Docker Support](./Step2.md)
- [Step 3 - Creating the Cluster](./Step3.md)
- [Step 4 - FrontEnd manually deploying to a Kubernetes Cluster](./Step4.md)
- [Step 5 - FrontEnd automating build/deployment process](./Step5.md)
