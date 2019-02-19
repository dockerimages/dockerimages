# dockerimages
General GUIDES about Docker based Deployments.

## How to Create a Permernent (Persisted) Deployment
To get a Persisted Configuration of your Deployment you need to describe it in some way good ways for this are:
- docker-compose
  - Create a docker-compose.yml file and store it in a folder of your HardDrive most of our images are already delivered with a 
  example docker-compose.yml so you can simply do ```git clone https://github.com/dockerimages/*``` inside of your desired
  storage location that will give you a copy of the image definition and assets if some are needed for additional
  configuration. After cloning the repo you should modify the docker-compose.yml and adjust it to your needs they are most time
  self explained or explaination can be found on public known additional resources. They are pointing by default to host 
  volumes in the current working directory to keep State and Configuration in same place and make it more easy to Scale 
  conditional. After the Modification you can start it with ```docker-compose up -d``` in the current working directory we 
  suggest creation of a folder structure like ```/srv/docker/*``` or ```~/.docker/*``` you can easy move the folders around as
  the volume configuration points to ```./*``` so its always the current directory if you are using containers as volumes
  your data will be stored most time on the docker host that executes the volume container ```/var/lib/docker/volumes/*``` if
  this is the case you know already what your doing so we will not discusse the up and down sides of doing so.
- Shell Script
  - Alternativ to the befor mentioned docker-compose definition you can simply create a Shell script with content like
  ```bash
  #!/bin/bash
  docker build -t imagename .
  docker run -d -v ./* --name containername imagename
  ```
  you can use all options that docker offers in that script the downside of this is that you could forget the containername so
  it adds a bit of maintance overhead as you need to review the file more often while docker-compose simply works always with
  the same command. The build is not needed if the image is already Published to a Registry in our case you can most time use
  ```dockerimages/*:tag``` directly.
- Advanced Configurations are Kubernetes, Swarm, OpenStack and other descriptive Cloud Deployments your on your own with this
:)
