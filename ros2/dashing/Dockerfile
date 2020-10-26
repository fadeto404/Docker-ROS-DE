# This is an auto generated Dockerfile for ros:ros1-bridge
# generated from docker_images_ros2/ros1_bridge/create_ros_ros1_bridge_image.Dockerfile.em
FROM ros:dashing-ros-base-bionic

# setup keys
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# setup sources.list
RUN echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros1-latest.list

ENV ROS1_DISTRO melodic
ENV ROS2_DISTRO dashing
# install ros packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-melodic-ros-comm=1.14.9-1* \
    ros-melodic-roscpp-tutorials=0.9.3-1* \
    ros-melodic-rospy-tutorials=0.9.3-1* \
    && rm -rf /var/lib/apt/lists/*

# install ros2 packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-dashing-ros1-bridge=0.7.6-1* \
    ros-dashing-demo-nodes-cpp=0.7.9-1* \
    ros-dashing-demo-nodes-py=0.7.9-1* \
    && rm -rf /var/lib/apt/lists/*

# install downstream packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    python-rosdep \
    && rm -rf /var/lib/apt/lists/*

# install intel realsense packages
RUN echo 'deb http://realsense-hw-public.s3.amazonaws.com/Debian/apt-repo xenial main' | tee /etc/apt/sources.list.d/realsense-public.list \
    && apt-key adv --keyserver keys.gnupg.net --recv-key 6F3EFCDE \
    && apt update \
    && apt install -y librealsense2-dkms \
    librealsense2-utils \
    librealsense2-dev \
    librealsense2-dbg \
    && apt install ros-dashing-cv-bridge ros-dashing-message-filters ros-dashing-image-transport \
    && apt install libssl-dev libusb-1.0-0-dev pkg-config libgtk-3-dev \
    && apt install libglfw3-dev libgl1-mesa-dev libglu1-mesa-dev \
    && apt install \
    && rm -rf /var/lib/apt/lists/*

# install rviz2
RUN apt update && apt install -y qt5-default ros-dashing-rviz2

# setup entrypoint
COPY ./ros_entrypoint.sh /
RUN ["chmod", "+x", "/ros_entrypoint.sh"]

