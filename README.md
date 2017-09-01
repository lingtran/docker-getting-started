# List of Docker commands
Curated while getting started with Docker

## Container level
### **Build and run app**

  #### Log into docker
  `docker login`

  #### Quick test of proper environment set up
  `docker run hello-world`

  #### Build app
  `docker build -t NAME-OF-APP`

  #### Run app
  * `docker run -p 4000:80 NAME-OF-APP`

    visit `http://localhost:4000`

  * `docker run -p 80:80 USERNAME/REPO:TAG`

    visit `http://localhost/`

  > Get container info `docker ps` after running the app, will list port

  > Can also get port info via `docker port CONTAINER-ID` or `docker port CONTAINER-NAME`

  #### Run app in background, in detached mode
  `docker run -d -p 4000:80 NAME-OF-APP`

  #### Stop process
  `docker stop CONTAINER-ID`

### **Docker image**

  #### Look at Docker image registry
  `docker images`

  #### Publish the image
  `docker push USERNAME/REPO:TAG`

  #### Pull and run image from remote repo
  `docker run -p 4000:80 USERNAME/REPO:TAG`

  #### Tag image
  `docker tag image USERNAME/REPO:TAG`

## Service level

  #### Run docker-compose.yml

  // Copy new/updated docker-compose.yml file before deploying the new/updated version
  * `docker-machine scp docker-compose.yml VM-NAME:~`


  * `docker stack deploy -c docker-compose.yml NAME-OF-APP`

    Run `docker swarm init` once before if it has not been done yet


  #### See list of containers just launched
  `docker stack ps NAME-OF-APP`

  #### Take down the app
  `docker stack rm NAME-OF-APP`

  #### Take down the swarm after the app
  `docker swarm leave --force`

## Swarms

  #### Use docker-machine and VirtualBox to create VMS
  `docker-machine create --driver virtualbox VM-NAME`

  #### See how to connect Docker Client to Docker engine running on a particular created VM
  `docker-machine env VM-NAME`

  #### Instruct VM to be a swarm manager
  Only a swarm manager can execute Docker commands

  `docker-machine ssh VM-NAME "docker swarm init"`
  * `docker-machine ssh` is a command that enables sending commands to a specified VM
  *  If error with need to use `--advertise-addr`, then `docker-machine ssh VM-NAME "docker swarm init --advertise-addr VM-IP:2377"`
  > `docker-machine ls` to find IP for appropriate VM-IP;

  > Specifying port has to be `2377`


  #### Join swarm
  Add worker to a swarm

  Workers are for capacity and are not able to execute Docker commands

  `docker-machine ssh VM-NAME "docker swarm join --token <token>"`
  > make sure specifying port is `2377`

  #### Check nodes in a swarm
  `docker-machine ssh VM-NAME` THEN in the machine, then run 'docker node ls' THEN to exit with command `exit`

  Alternatively, `docker-machine ssh VM-NAME "docker node ls"`

  #### Leave swarm
  `docker-machine ssh VM-NAME "docker swarm leave"`

### **Deploy app on a cluster**
  `docker-machine scp docker-compose.yml VM-NAME:~`

  `docker-machine ssh VM-NAME "docker stack deploy -c docker-compose.yml NAME-OF-APP"`

  Check via `docker-machine ssh VM-NAME "docker stack ps NAME-OF-APP"`

### **Access cluster**
  `docker-machine ls`

### **Cleanup**
  `docker-machine ssh VM-NAME "docker stack rm NAME-OF-APP"`

  Can choose to keep the swarm or remove it

## Stacks

### **Visualizer service**
  Run `docker-machine ls` to get IP address of one of nodes

  In this version, visualizer runs on port 8080, so visit either IP address at this port.
