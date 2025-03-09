# How to install ros2 foxy

OS : wsl2-ubuntu20.04

1. Setup locale

$ sudo apt update && sudo apt install locales

$ sudo locale-gen en_US en_US.UTF-8

$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8

$ export LANG=en_US.UTF-8

2. setup source

$ sudo apt update && sudo apt install curl gnupg2 lsb-release

$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

3. install ros2 package

$ sudo apt update

$ sudo apt install ros-foxy-desktop ros-foxy-rmw-fastrtps* ros-foxy-rmw-cyclonedds*

4. 


