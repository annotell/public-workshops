# Set up your environment
1. Download or `git clone` the repository https://github.com/annotell/public-workshops
Open a terminal and cd to the repository location and into the ship-it folder. From here we will run all our commands
    ```
    $ cd ship-it
    ```

1. Check out the code in the browser; open the file://<full-path-to-repo>/public-workshops/ship-it/src/index.html in your browser and take a look around

Put code in a container

We picked a simple responsive webpage from a template at https://html5up.net/

from here we will run all our commands
cd ship-it

docker build -t datatjej:1.0 .

docker images

docker run -d -p 80:80 datatjej:1.0

visit localhost:80 in your browser

Make some changes to the code (for example, pick a new picture maybe from https://unsplash.com/)

Once you've updated the code you need to build a new docker image that contains the updated code

Note the new version tag in the two following commandos

docker build -t datatjej:1.1 .

docker run -d -p 81:80 datatjej:1.1

go back to localhost:81 and refresh the page, see that your changes has been applied


clean up by stopping your container in docker
docker ps
docker stop {image_id or image_name}
docker rm {image_id or image_name}
➜  ship-it git:(main) ✗ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                NAMES
ad497457d42e   datatjej:1.0   "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:80->80/tcp   stupefied_tesla
➜  ship-it git:(main) ✗ docker stop stupefied_tesla && docker rm stupefied_tesla
stupefied_tesla
stupefied_tesla


Congratualations! You have successfully packaged your code in a container! :clap: