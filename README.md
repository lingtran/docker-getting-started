## Log into docker
`docker login`

## Quick test of proper environment set up
`docker run hello-world`

## Build app
`docker build -t NAME-OF-APP`

## Run app
* `docker run -p 4000:80 NAME-OF-APP`

  visit `http://localhost:4000`

* `docker run -p 80:80 USERNAME/REPO:TAG`

  visit `http://localhost/`

## Run app in background, in detached mode
`docker run -d -p 4000:80 NAME-OF-APP`

## Look at Docker image registry
`docker images`

## Publish the image
`docker push USERNAME/REPO:TAG`

## Pull and run image from remote repo
`docker run -p 4000:80 USERNAME/REPO:TAG`

## Tag image
`docker tag image USERNAME/REPO:TAG`

## Stop process
`docker stop CONTAINER-ID`
