Time to clean up!

minikube stop
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)