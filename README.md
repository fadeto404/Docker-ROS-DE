# Docker-ROS-DE
Dockerfiles for building images for development with ROS2 and ROS1. GUI support and device access support (both unsafe) exist.

## Building an image
1. Clone this repo
2. Open the directory of the distribution you want to build an image of
3. Run `sudo docker build -t image_name:image_tag .` in that directory

## Creating a container
_Do this only once!_
***For GUI and device support read the sections below before running the commands***

Create a directory for your ROS workspace, or alternatively a folder for multiple ROS workspaces if you're brave
`mkdir /path/to/my/ws`
We will create a "volume" to share this directory between the container and the host OS.
Enter the workspace directory
`cd /path/to/my/ws`

***If you only need ROS nodes inside the container,*** run:
`sudo docker run --env DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 --volume /tmp/.X11-unix:/tmp/.X11-unix --volume /path/to/my/ws:/ws --name <container_name> -it image_name:image_tag`
replacing the `<container_name>` with a name of your choice, as well as the path and image.

If you want the container to communicate with other containers, other programs running on the host, or with other computers on the network, ports will need to be opened. Probably this means ports 22222-22225 (UDP). See more here: 
* [6.7. Listening Locators — Fast DDS 2.0.0 documentation](https://fast-rtps.docs.eprosima.com/en/latest/fastdds/transport/listening_locators.html)
* [What default ports are used in ROS2 DDS implementations? - ROS Answers: Open Source Q&A Forum](https://answers.ros.org/question/295400/what-default-ports-are-used-in-ros2-dds-implementations/)
* [How to run example talker/listener on 2 machines with different ipaddr? - Next Generation ROS - ROS Discourse](https://discourse.ros.org/t/how-to-run-example-talker-listener-on-2-machines-with-different-ipaddr/2106)

Opening ports for the docker container is done with:
1. For communicating with other containers or processes on the host only:
`sudo docker run --env DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 --volume /tmp/.X11-unix:/tmp/.X11-unix --volume /path/to/my/ws:/ws --name <container_name> -p 22222-22225/udp -p 11311 -it image_name:image_tag`
2. For communicating with other machines on the network as well as the above:
`sudo docker run --env DISPLAY=$DISPLAY --env QT_X11_NO_MITSHM=1 --volume /tmp/.X11-unix:/tmp/.X11-unix --volume /path/to/my/ws:/ws --name <container_name> -p 22222-22225:22222-22225/udp -p 11311:11311 -it image_name:image_tag`

### Enabling GUI support
To fully enable GUI there are a few options:
1. The lazy, easy, reckless version
    Run `xhost +local:root` on the host machine to enable others to use the X11 socket. Run `xhost -local:root` when you're done.
2. The slightly safer option. Run the following
 ```bash 
export containerId=$(docker ps -l -q) # Assumes that the docker container was the most recently started. Otherwise set $containerId=<container_id>$
xhost +local:`docker inspect --format='{{ .Config.Hostname }}' $containerId`
sudo docker start $containerId
 ```
3. More found at: [docker/Tutorials/GUI - ROS Wiki](http://wiki.ros.org/docker/Tutorials/GUI)

### Enabling devices
A few options:
1. Use the flag `--privileged` during the `sudo docker run ...`
2. Use the flag `--device` and specify which device, when running `sudo docker run ...`

### Notes in special cases:
1. ROS1: Be aware that the `ROS_MASTER_URI` may have to be changed according to your setup. Check with `printenv`.
2. ROS2: If you have multiple systems using DDS on the same network, you can use a domain ID to separate them. Run `export ROS_DOMAIN_ID=xxx`, replacing `xxx` with a number between 0 and 255, on every machine running ROS2 nodes.
3. ROS2: The devices must also be on the same multicast network. If they are not there is a suggestion in the 3rd link above.

## Starting and stopping a container
To start an existing container, run:
`sudo docker start -i <container_name>`

To stop a running container, run:
`sudo docker stop <container_name>`

## Executing commands in containers
In general:
`sudo docker exec <container_name> <command>`

The most important one will probably be opening a terminal in your container. This is done by:
`sudo docker exec -it <container_name> bash`


