#docker-dojo
Generate Docker Image
======================

* Building the image 

```bash
cd app
docker build -t maneta/sinatra .
```
* Commiting the image to Docker Hub

```bash
docker push maneta/sinatra
```

* Repository: https://hub.docker.com/r/maneta/sinatra/

Deploying Redis Cluster
========================

Creating Master Controller
--------------------------

```bash
kubectl create -f redis-master-controller.yaml
```

* Verify that the master is running:

```bash
kubectl get pods
```

* Output:

```bash
NAME                 READY     REASON    RESTARTS   AGE
redis-master-5y3pb   1/1       Running   0          36s
```

Creating Master Service
------------------------

```bash
kubectl create -f redis-master-service.yaml
```

* Verify that the slaves are running:

```bash
kubectl get pods
```

* Output:

```bash
ME                READY     STATUS    RESTARTS   AGE
redis-master-gti95  1/1       Running   0          5m
redis-slave-lmux8   1/1       Running   0          44s
redis-slave-suafd   1/1       Running   0          44s
```

