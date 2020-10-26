# This is an auto generated Dockerfile for ros:ros1-bridge
# generated from docker_images_ros2/ros1_bridge/create_ros_ros1_bridge_image.Dockerfile.em
FROM ros:eloquent-ros-base-bionic

# setup keys
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654

# setup sources.list
RUN echo "deb http://packages.ros.org/ros/ubuntu bionic main" > /etc/apt/sources.list.d/ros1-latest.list

ENV ROS1_DISTRO melodic
ENV ROS2_DISTRO eloquent
# install ros packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-melodic-ros-comm=1.14.9-1* \
    ros-melodic-roscpp-tutorials=0.9.3-1* \
    ros-melodic-rospy-tutorials=0.9.3-1* \
    && rm -rf /var/lib/apt/lists/*

# install ros2 packages
RUN apt-get update && apt-get install -y --no-install-recommends \
    ros-eloquent-ros1-bridge=0.8.2-1* \
    ros-eloquent-demo-nodes-cpp=0.8.4-1* \
    ros-eloquent-demo-nodes-py=0.8.4-1* \
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
    && rm -rf /var/lib/apt/lists/*

# install rviz2; NOTE: Compiling takes a long time ._.
RUN apt install -y ros-eloquent-rviz2 \
    && export LD_LIBRARY_PATH=/opt/ros/eloquent/opt/rviz_ogre_vendor/lib:$LD_LIBRARY_PATH

#RUN apt install -y libxaw7 libxaw7-dev libxaw7-dbg libogre-1.9-dev libglu1-mesa-dev freeglut3-dev mesa-common-dev freeglut3 libgl1-mesa-dev libglu1-mesa-dev qt5-default ros-eloquent-yaml-cpp-vendor ros-eloquent-interactive-markers ros-eloquent-laser-geometry ros-eloquent-map-msgs \
#    && mkdir /workspaces/eloquent/src \
#    && cd /workspaces/eloquent/src \
#    && git clone https://github.com/ros2/rviz.git -b eloquent \
#    && cd .. \
#    && colcon build --merge-install
#    # TODO: change "resource_retriever::resource_retriever" to "resource_retriever" in CMakeLists of rviz_rendering, rviz_rendering_tests, and rviz_default_plugins 

# setup entrypoint
COPY ./ros_entrypoint.sh /
RUN ["chmod", "+x", "/ros_entrypoint.sh"]

