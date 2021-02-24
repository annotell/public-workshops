# The Clean Up!

In order to stop minikube from running and all containers inside minikube, run the following command:
```bash
$ minikube stop
```

In order to stop the containers we ran locally with `docker run`, open a new terminal and do the following:
```bash
$ docker stop $(docker ps -a -q)
```
```bash
$ docker rm $(docker ps -a -q)
```
If you want to clean out all the resources created in this workshop take a look at the following steps. BE AWARE, it will remove ALL docker images on your local computer. 
To delete all docker images we created with `docker build -t datatjej:1.0 .`, run:
```bash
$ docker rmi $(docker images -a -q)
```
If you don't want to use the local minikube cluster again, you can also clean out the cluster by running:
```bash
$ minikube delete
```

All done!