# Step 2 - FrontEnd team adding Docker Support

FrontEnd team is responsible for a small part of the whole solution build by the company. Others teams will build services that might be, direct or indirectally, dependents on their services.

They needed a place to deploy their applications with security, rolling updates, networking, discovery, capable of running multiple stacks (they wish to migrate their web FrontEnd to Angular in the future).

Containers and Kubernetes solve many of this problem by providing a reliable and secure way to run application across a number of machines.

Visual Studio tooling makes it easy to start working with Docker. For that right click on each project and select Add &rarr; Container Orchestrator Support.

This will create a Dockerfile with instructions on how to build the docker image and create a docker-compose project that allow us to debug multiple containers inside Visual Studio.

## Running containers in Kubernetes

Kubernetes orchestrates containers in a cluster. In order to run a container in a Kubernetes cluster (assuming you have one already) requires the following steps:

1. From your source code build a docker image
1. Publish docker image to an image registry (Docker Hub, Azure Container Registry)
1. Create the application manifests (yaml files) and apply to Kubernetes

Kubernetes can be executed locally (for testing purposes) with [minikube](https://kubernetes.io/docs/setup/minikube/) or [Docker CE](https://docs.docker.com/docker-for-windows/kubernetes/).

I will be using Docker for now, but this example can be applied to minikube same way.

1. Build an image with Visual Studio. Click Build / Batch Build... and select "docker-compose" with Release configuration. Click "Build" button. After the build is done you should see 2 new images by running ```docker images```: frontendapi:latest and frontendweb:latest.
1. Before publishing we need to tag the images, adding a version and the container registry information (fbeltrao in my case):
```
docker tag frontendapi:latest fbeltrao/frontendapi:1.0 & docker tag frontendweb:latest fbeltrao/frontendweb:1.0
```
Now we can publish the images to Docker Hub (it requires ```docker login``` the first time):
```
docker push fbeltrao/frontendapi:1.0 & docker push fbeltrao/frontendweb:1.0
```
3. Apply the deployment to kubernetes using the kubectl command line. To view the yaml file content [click here](https://github.com/containers-on-azure/FrontEnd/blob/version-01/deployment/k8s/local-deployment.yaml)
```cmd
kubectl apply -f https://raw.githubusercontent.com/containers-on-azure/FrontEnd/version-01/deployment/k8s/local-deployment.yaml
```

You can check that the web service is running:
```cmd
$ kubectl get services
NAME           TYPE           CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
frontend-api   ClusterIP      10.107.213.245   <none>        80/TCP         18s
frontend-web   LoadBalancer   10.103.94.135    localhost     80:30392/TCP   18s
kubernetes     ClusterIP      10.96.0.1        <none>        443/TCP        4h
```

Open the browser where the web is bounded (in my case http://localhost:80) and check that the application is running.


[Go to Start](./ReadMe.md)\
[Go to previous step](./Step1.md)\
[Go to next step](./Step3.md)