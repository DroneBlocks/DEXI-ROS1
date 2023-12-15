# ATS-5

docker run -it --rm -v ${PWD}:/root/ros_ws/src ros:noetic

cd ~/ros_ws

sudo apt update

### Install ros_led locally

cd ~/ros_ws/src
git clone https://github.com/copterexpress/ros_led

cd ..

rosdep install --from-paths src --ignore-src -r -y

catkin_make

source devel/setup.bash

roslaunch ats5 led.launch

## Test LEDs

rosservice call /led/set_effect "{effect: 'rainbow'}"
rosservice call /led/set_effect "{effect: 'rainbow_fill'}"

# Camera Config

sudo apt install ros-noetic-cv-camera
rosrun cv_camera cv_camera_node

# Web Video

sudo apt install ros-noetic-web-video-server
rosrun web_video-server web_video_server
http://n.n.n.n:8080
