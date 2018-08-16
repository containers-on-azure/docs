# Step 2 - FrontEnd team adding Docker Support

## Goal

FrontEnd team is responsible for a small part of the whole solution build by the company. Others teams will build services that might be, direct or indirectally, dependents on their services.

They needed a place to deploy their applications with security, rolling updates, networking, discovery, capable of running multiple stacks (they wish to migrate their web FrontEnd to Angular in the future).

Containers and Kubernetes solve many of this problem by providing a reliable and secure way to run application across a number of machines.

Visual Studio tooling makes it easy to start working with Docker. For that right click on each project and select Add &rarr; Container Orchestrator Support.

This will create a Dockerfile with instructions on how to build the docker image and create a docker-compose project that allow us to debug multiple containers inside Visual Studio.

### Running containers in Kubernetes

Kubernetes orchestrates containers in a cluster. In order to run a container in a Kubernetes cluster (assuming you have one already) requires the following steps:

1. From your source code build a docker image
1. Publish docker image to an image registry (Docker Hub, Azure Container Registry)
1. Create the application manifests (yaml files) and apply to Kubernetes

Kubernetes can be executed locally (for testing purposes) with [minikube](https://kubernetes.io/docs/setup/minikube/) or [Docker CE](https://docs.docker.com/docker-for-windows/kubernetes/).

I will be using minikube for now, but this example can be applied to Docker CE the same way.

1. Build an image with Visual Studio. Click Build / Batch Build... and select "docker-compose" with Release configuration. Click button "Build". After the build is done you should see 2 new images by running ```docker images```: frontendapi:latest and frontendweb:latest.
1. Before we publish we need to tag the image, adding a version and the registry information (fbeltrao in my case):
```
docker tag frontendapi:latest fbeltrao/frontendapi:1.0
docker tag frontendweb:latest fbeltrao/frontendweb:1.0
```
Now we can publish the images to Docker Hub (it requires ```docker login``` the first time):
```
docker push fbeltrao/frontendapi:1.0
docker push fbeltrao/frontendweb:1.0
```
3. Create the application manifest yaml, describing how your application works.
```yaml
```
kubectl apply -f "C:\dev\github.com\containers-on-azure\FrontEnd\deployment\minikube\deployment.yaml"

kubectl expose deployment frontend-deployment --type=LoadBalancer
service "frontend-deployment" exposed
kubectl get services
NAME                  TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
frontend-deployment   LoadBalancer   10.103.232.109   <pending>     80:32014/TCP   5s
kubernetes            ClusterIP      10.96.0.1        <none>        443/TCP        53m

minikube service frontend-deployment -> /api/v1/contents



## Projects

|Project|Description|Stack|Dependencies|Branch|
|-|-|-|-|-|
|[FrontEnd.Web](https://github.com/containers-on-azure/FrontEnd)|Web UI|ASP.NET Razor Pages|FrontEnd.Api|version-00|
|[FrontEnd.Api](https://github.com/containers-on-azure/FrontEnd)|Web API|ASP.NET Web Api||version-00|

[FrontEnd.Web] &rarr; [FrontEnd.Api]

To debug the application run both projects in Visual Studio. Open the browser on http://localhost:5100/ which will show you the start page containing information about Stocks Market. This information is being pulled from http://localhost:5200/api/v1/contents. The base URI of the API is defined in the configuration setting ```FrontEndApi```, found in file ```appsettings.Development.json``` in FrontEnd.Web project.

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "System": "Information",
      "Microsoft": "Information"
    }
  },
  "FrontEndApi": "http://localhost:5200",
  "Kestrel": {
    "EndPoints": {
      "Http": {
        "Url": "http://localhost:5100"
      },
      "Https": {
        "Url": "https://localhost:5101"
      }
    }
  }
}
```

[Go to Start](./ReadMe.md)\
[Go to previous step](./ReadMe.md)\
[Go to next step](./Step2.md)