# Docker DE cheatsheet

## Dashing
**Build the image**
`sudo docker build -t ros:dashing-ros1-bridge-de .`

**Running a new container**
Make sure to replace the path name to your workspace
`sudo docker run --privileged --env DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 --volume /tmp/.X11-unix:/tmp/.X11-unix --volume /home/rns/Documents/Robotics/semester5/p5/workspaces:/workspaces --name dashing-de -p 22222-22225:22222-22225/udp -p 11311:11311 -it ros:dashing-ros1-bridge-de`

**Starting an existing container**
`sudo docker start -i dashing-de`

**New terminal in container**
`sudo docker exec -it dashing-de bash`

**Preparing for running**
ROS recommends running nodes in a different terminal from the one where you built the nodes
`cd /workspaces/dashing && . install/setup.bash`

## Eloquent
**Build the image**
`sudo docker build -t ros:eloquent-ros1-bridge-de .`

**Running a new container**
Make sure to replace the path name to your workspace
`sudo docker run --privileged --env DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 --volume /tmp/.X11-unix:/tmp/.X11-unix --volume /home/rns/Documents/Robotics/semester5/p5/workspaces:/workspaces --name eloquent-de -p 22222-22225:22222-22225/udp -p 11311:11311 -it ros:eloquent-ros1-bridge-de`

**Starting an existing container**
`sudo docker start -i eloquent-de`

**New terminal in container**
`sudo docker exec -it eloquent-de bash`

**Preparing for running**
ROS recommends running nodes in a different terminal from the one where you built the nodes
`cd /workspaces/eloquent && . install/setup.bash`

## Foxy
**Build the image**
`sudo docker build -t ros:foxy-ros1-bridge-de .`

**Running a new container**
Make sure to replace the path name to your workspace
`sudo docker run --privileged --env DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 --volume /tmp/.X11-unix:/tmp/.X11-unix --volume /home/rns/Documents/Robotics/semester5/p5/workspaces:/workspaces --name foxy-de -p 22222-22225:22222-22225/udp -p 11311:11311 -it ros:foxy-ros1-bridge-de`

**Starting an existing container**
`sudo docker start -i foxy-de`

**New terminal in container**
`sudo docker exec -it foxy-de bash`

**Preparing for running**
ROS recommends running nodes in a different terminal from the one where you built the nodes
`cd /workspaces/foxy && . install/setup.bash`

# General docker
## Running a container from an image
```docker run <image-name>```
Brug ```-d``` for at detache fra containerens stdout

## List containers
```docker ps``` eller ```docker container ls``` for at se kørende containers. Brug -a eller --all for at se alle containers inkl. dem der ikke kører

## Stop a container
```docker stop <id/container-name>```
Returns the name if succesful 

## Start a container
```docker start <container>```
Returns \<container> if succesful

## Restart a running container
```docker restart <container>```
Returns \<container> if succesful

## Delete a container
```docker rm <id/container-name>```
Removes a stopped container permanently
Returns the name if succesful

## List images
```docker images``` eller ```docker image ls``` for at se downloadede images.

## Delete an image
```docker rmi <image-name>```
Det er vigtigt at ingen containere baseret på dette image eksisterer. Fjern disse først hvis nogle findes.

## Download an image
```docker pull <image-name>``` for at downloade et image uden at kører en container
```docker run <image-name>``` vil automatisk downloade et image hvis det ikke findes lokalt allerede

## Execute a command on a running docker container
```docker exec <container> <command>```
Eksempelvis kan man bruge bash for at få adgang til en shell inden i containeren

```docker exec -it <container> bash```

## Attaching to a containers stdout
```docker attach <container>```
