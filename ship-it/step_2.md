Next step will be to instead of running the docker container on you local computer, see how it would look when running it in kubernetes. 
Usually Kubernetes is run in the cloud and over multiple instances, but for the sake of this workshop we'll use minikube which similates a Kubernetes cluster on your local computer. 

minikube start
(this might take a couple of minutes)

➜  ~ minikube start
😄  minikube v1.15.1 on Darwin 10.15.7
✨  Using the docker driver based on existing profile
👍  Starting control plane node minikube in cluster minikube
🔄  Restarting existing docker container for "minikube" ...
🐳  Preparing Kubernetes v1.19.4 on Docker 19.03.13 ...
🔎  Verifying Kubernetes components...
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default



Minikube docker has it's own context, we need to rebuild our docker image (or pull for a remote repository(which we don't have now)) in the minikube context! So let's start with that:

Set up the minikube docker context:
eval $(minikube docker-env)

rebuild the docker image, but let's pick a new tag:
docker build -t datatjej:2.0 .

make sure the image exists in the docker daemon (docker images | grep datatjej) check the tag


make sure the .yaml points to the right image, 

```yaml
      containers:
      - name: datatjej
        image: datatjej:2.0
```


$ kubectl apply -f datatjej-deployment.yaml --dry-run=client
deployment.apps/datatjej created (dry run)

$ kubectl apply -f datatjej-deployment.yaml
deployment.apps/datatjej created

kubectl get deployments
NAME       READY   UP-TO-DATE   AVAILABLE   AGE
datatjej   2/2     2            2           27s


each pod maps one "docker run" on your laptop
kubectl get pods 
NAME                        READY   STATUS    RESTARTS   AGE
datatjej-5564cc49c5-h5n6d   1/1     Running   0          60s
datatjej-5564cc49c5-t5zg4   1/1     Running   0          60s

the next step is to expose our application with a service

kubectl apply -f datatjej-service.yaml --dry-run=client
service/datatjej configured (dry run)

kubectl apply -f datatjej-service.yaml
service/datatjej created

kubectl get service datatjej

*** We can see that the service has two endpoints, mapping to our two pods
kubectl get endpoints datatjej
NAME       ENDPOINTS                         AGE
datatjej   172.17.0.3:8080,172.17.0.4:8080   4h28m

kubectl get pods -o wide
NAME                        READY   STATUS    RESTARTS   AGE   IP           NODE       NOMINATED NODE   READINESS GATES
datatjej-7d74b7c88c-k2sx5   1/1     Running   0          65m   172.17.0.3   minikube   <none>           <none>
datatjej-7d74b7c88c-vglrc   1/1     Running   0          39s   172.17.0.4   minikube   <none>           <none>

**** compare output of pods with list of endpoints, they should match

We now have a service, and it's backed by two different pods! This allows us to have a higher available application since we can lose one of the pods and still servce traffic. But by just setting up a service like this, we're not exposing our application outside the minikube kubernetes cluster context, so in order to access the website, we need to set up a link to the service via minikube, once that is done, we can now view our website via the URL minikube returns, open the link in the browser

$ minikube service --url datatjej
😿  service default/datatjej has no node port
🏃  Starting tunnel for service datatjej.
|-----------|----------|-------------|------------------------|
| NAMESPACE |   NAME   | TARGET PORT |          URL           |
|-----------|----------|-------------|------------------------|
| default   | datatjej |             | http://127.0.0.1:63093 |
|-----------|----------|-------------|------------------------|
http://127.0.0.1:63093
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

ctrl+c to exit the tunnel

