Put code in a container

We picked a simple responsive webpage from a template at https://html5up.net/

docker build -t datatjej:1.0 .

docker images

docker run -p 8080:8080 datatjej:1.0

visit localhost:8080 in your browser

Make some changes to the code (for example, pick a new picture maybe from https://unsplash.com/)

Once you've updated the code you need to build a new docker image that contains the updated code

Note the new version tag in the two following commandos

docker build -t datatjej:1.1 .

docker run -p 8080:8080 datatjej:1.1

go back to localhost:8080 and refresh the page, see that your changes has been applied

Congratualations! You have successfully packaged your code in a container! :clap: