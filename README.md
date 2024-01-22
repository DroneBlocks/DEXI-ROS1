# DEXI

## Docker for local development

docker run -it --rm -v ${PWD}:/root/ros_ws/src ros:noetic

cd ~/ros_ws

sudo apt update

## Install ros_led locally

cd ~/ros_ws/src
git clone https://github.com/copterexpress/ros_led

## Build

cd ..

rosdep install --from-paths src --ignore-src -r -y

catkin_make

source devel/setup.bash

roslaunch dexi led.launch

## Test LEDs

Make sure to set permissions for LED control:
sudo chown root:root $(catkin_find ws281x ws281x_node)
sudo chmod +s $(catkin_find ws281x ws281x_node)

rosservice call /led/set_effect "{effect: 'rainbow'}"
rosservice call /led/set_effect "{effect: 'rainbow_fill'}"

## Camera & Web Video Setup

1. sudo apt install libxmlrpcpp-dev
2. sudo apt install librosconsole-dev
3. Add start_x=1 to /boot/firmware/config.txt and reboot
4. Make waitfile executable: chmod +x ~/ros_ws/src/dexi/dexi/src/waitfile 
5. Test camera: rosrun cv_camera cv_camera_node
6. Test web video: rosrun web_video_server web_video_server
7. Access here: http://n.n.n.n:8080

## Run all DEXI nodes

roslaunch dexi dexi.launch

## nginx for topic viewer

docker run -it --rm -d -p 80:80 --name web -v ~/ros_ws/src/dexi/dexi/www:/usr/share/nginx/html nginx

## nginx for DroneBlocks
docker run -it --rm -d -p 80:80 --name droneblocks -v ~/ros_ws/src/dexi/droneblocks/www:/usr/share/nginx/html nginx
