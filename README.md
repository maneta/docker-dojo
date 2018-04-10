docker-dojo
===========

Generate Docker Image
======================

* Building the image 

```bash
cd app
docker build -t maneta/sinatra .
```

* Run the Container Image 

```
docker run --rm -t -p 4567:4567  maneta/sinatra
```

* Pushing the Docker image to Docker Hub

```bash
docker push maneta/sinatra
```

* Repository: https://hub.docker.com/r/maneta/sinatra/

Useful commands:

All running dockers:

```
docker ps
```

All running and stopped dockers:

```
docker ps -a
```

Kill a container:

```
docker kill ${containerID}
```

Remove a container:

```
docker rm ${containerID}
```

List Docker Images:

```
docker images
```

Remove Docker image:

```
docker rmi ${imageID}
```

Docker Compose
===============

* Start the docker compose:

```bash
cd compose
docker-compose up
```

* Shut Down the Compose

```bash
cd compose
docker-compose down
```

K8´s Deploy (Google Cloud)
==========================

* All the configurations files are located on the k8s-conf-files directory

Creating Disk
--------------

```bash
gcloud compute disks create --size 200GB redis-disk
```

* Output: 

```bash
Created [https://www.googleapis.com/compute/v1/projects/ruby-app-1470156911832/zones/europe-west1-b/disks/redis-disk].
NAME        ZONE            SIZE_GB  TYPE         STATUS
redis-disk  europe-west1-b  200      pd-standard  READY
```

Creating Redis Controller
--------------------------

```bash
kubectl create -f redis-controller.yml
```

* Verify that the Redis Controller is running:

```bash
kubectl get pods
```

* Output:

```bash
NAME          READY     STATUS    RESTARTS   AGE
redis-q0ifr   1/1       Running   0          1m
```

Creating Redis Service
------------------------

```bash
kubectl create -f redis-service.yml
```

* Verify that the Redis service is running:

```bash
kubectl get services
```

* Output:

```bash
NAME         CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
kubernetes   10.59.240.1    <none>        443/TCP    2h
redis        10.59.255.11   <none>        6379/TCP   1m
```


Creating Sinatra Controller
--------------------------

```bash
kubectl create -f sinatra-controller.yml
```

* Verify that the Sinatra Controller is running:

```bash
kubectl get pods
```

* Output:

```bash
NAME            READY     STATUS    RESTARTS   AGE
redis-q0ifr     1/1       Running   0          7m
sinatra-e3n4t   1/1       Running   0          1m
sinatra-h59za   1/1       Running   0          1m
```

Creating Sinatra Service
------------------------

```bash
kubectl create -f sinatra-service.yml
```

* Verify that the Sinatra service is running:

```bash
kubectl get services
```

* Output:

```bash
NAME         CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
kubernetes   10.59.240.1    <none>        443/TCP    2h
redis        10.59.255.11   <none>        6379/TCP   1m
```

* Get Load Balancer Public IP

```bash
kubectl describe services frontend | grep "LoadBalancer Ingress"
```

* Output:

```bash
LoadBalancer Ingress:	104.155.27.74
```

Openshift Deployment
====================

* All the configurations files are located on the k8s-conf-files directory

Creating Persistent Volume Claim
---------------------------------

```bash
oc create -f pvc.yml
```


Creating Redis Controller
--------------------------

```bash
oc create -f redis-controller.yml
```

Creating Redis Service
------------------------

```bash
kubectl create -f redis-service.yml
```

