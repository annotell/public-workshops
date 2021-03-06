# Packaging the Code

We know our code! And it works in the browser. But what if we want to package this so that we can run the code *anywhere*. 

1. Make sure you're in the right folder in your terminal by running:
    ```bash
    $ pwd
    ```
    Example output:
    ```bash
    /Users/hannastrang/code/public-workshops/ship-it
    ```

1. Let's begin with creating a docker image containing our code, based on the [Dockerfile](./Dockerfile).
    ```bash
    $ docker build -t datatjej:1.0 .
    ```
1. We should now be able to see that this docker image is created by listing docker images
    ```bash
    $ docker images
    ```
1. And now, let's spin up this container locally! This command tells docker to run a container from the image called `datatjej` with the tag `1.0`, connecting container port 80 to your local port 80, and `-d` means run it in the background.
    ```bash
    $ docker run -d -p 80:80 datatjej:1.0
    ```
1. We should now have a container running, serving our application on localhost:80 in your browser, try it out by pasting `localhost:80` into your browser address field.

1. Make some changes to the code (for example, pick a new picture maybe from https://unsplash.com/)

1. Once you've updated the code you need to build a new docker image that contains the updated code.

     Note the new version tag in the two following commandos
    ```bash
    $ docker build -t datatjej:1.1 .
    ```
    ```bash
    $ docker run -d -p 81:80 datatjej:1.1
    ```
1. Go back to localhost:80 and change it to localhost:81, which is connecting container port 80 to your local port 81, see that your changes has been applied



Congratualations! You have successfully packaged your code in a container! :clap:

Return to the [workshop guidelines](./README.md)

