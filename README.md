# ATS-5

docker run -it --rm -v ${PWD}:/root/ros_ws/src ros:noetic

cd ~/ros_ws

sudo apt update

rosdep install --from-paths src --ignore-src -r -y

catkin_make
