# The Clean Up!

In order to stop minikube from running and all containers inside minikube, run the following command:
```bash
$ minikube stop
```

In order to stop the containers we ran locally with `docker run`, do the following:
```bash
$ docker stop $(docker ps -a -q)
```
```bash
$ docker rm $(docker ps -a -q)
```

All done!