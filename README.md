# How to install ros2 Jazzy

OS : wsl2-ubuntu24.04

## Set locale
```bash
$ sudo apt update && sudo apt install locales
$ sudo locale-gen en_US en_US.UTF-8
$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
$ export LANG=en_US.UTF-8
$ locale  # verify settings
```
## Enable required repositories
```bash
$ sudo apt install software-properties-common
$ sudo add-apt-repository universe
$ sudo apt update && sudo apt install curl -y
$ export ROS_APT_SOURCE_VERSION=$(curl -s https://api.github.com/repos/ros-infrastructure/ros-apt-source/releases/latest | grep -F "tag_name" | awk -F\" '{print $4}')
$ curl -L -o /tmp/ros2-apt-source.deb "https://github.com/ros-infrastructure/ros-apt-source/releases/download/${ROS_APT_SOURCE_VERSION}/ros2-apt-source_${ROS_APT_SOURCE_VERSION}.$(. /etc/os-release && echo ${UBUNTU_CODENAME:-${VERSION_CODENAME}})_all.deb"
$ sudo dpkg -i /tmp/ros2-apt-source.deb 
```
## Install ros development tools
```bash
$ sudo apt update && sudo apt install ros-dev-tools
```
## install ros2 package
```bash
$ sudo apt update
$ sudo apt upgrade
$ sudo apt install ros-jazzy-desktop
$ sudo apt install ros-jazzy-ros-base
``` 
## install development tools
```bash
$ sudo apt update && sudo apt install -y build-essential cmake git libbullet-dev python3-colcon-common-extensions python3-flake8  python3-pip python3-pytest-cov python3-rosdep python3-setuptools python3-vcstool wget
$ python3 -m pip install -U argcomplete flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest-repeat pytest-rerunfailures pytest
$ sudo apt install --no-install-recommends -y libasio-dev libtinyxml2-dev libcunit1-dev
```
## add to .bashrc
```bash
# ros2 init
source /opt/ros/jazzy/setup.bash
source ~/ros2_ws/install/local_setup.bash
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
source /usr/share/vcstool-completion/vcs.bash
source /usr/share/colcon_cd/function/colcon_cd.sh
export LIBGL_ALWAYS_SOFTWARE=1
export _colcon_cd_root=~/ros2_ws 
export ROS_DOMAIN_ID=0
export ROS_NAMESPACE=rapi5-0
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
export RCUTILS_COLORIZED_OUTPUT=1 
export RCUTILS_LOGGING_USE_STDOUT=0 
export RCUTILS_LOGGING_BUFFERED_STREAM=1
```
## Setup environment
```bash
$ source /opt/ros/jazzy/setup.bash
```
## Try some examples
```bash
# In one terminal, source the setup file and then run a C++
$ source /opt/ros/jazzy/setup.bash
$ ros2 run demo_nodes_cpp talker
# In another terminal source the setup file and then run a Python
$ source /opt/ros/jazzy/setup.bash
$ ros2 run demo_nodes_py listener
```

# How to install ros2 foxy

OS : wsl2-ubuntu20.04

## Setup locale
```bash
$ sudo apt update && sudo apt install locales
$ sudo locale-gen en_US en_US.UTF-8
$ sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
$ export LANG=en_US.UTF-8
```

## setup source
```bash
$ sudo apt update && sudo apt install curl gnupg2 lsb-release
$ sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
$ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```
## install ros2 package
```bash
$ sudo apt update
$ sudo apt install ros-foxy-desktop ros-foxy-rmw-fastrtps* ros-foxy-rmw-cyclonedds* 
```
## install development tools
```bash
$ sudo apt update && sudo apt install -y build-essential cmake git libbullet-dev python3-colcon-common-extensions python3-flake8  python3-pip python3-pytest-cov python3-rosdep python3-setuptools python3-vcstool wget
$ python3 -m pip install -U argcomplete flake8-blind-except flake8-builtins flake8-class-newline flake8-comprehensions flake8-deprecated flake8-docstrings flake8-import-order flake8-quotes pytest-repeat pytest-rerunfailures pytest
$ sudo apt install --no-install-recommends -y libasio-dev libtinyxml2-dev libcunit1-dev
```
## add to .bashrc
```bash
# ros2 init
source /opt/ros/foxy/setup.bash
source ~/ros2_ws/install/local_setup.bash
source /usr/share/colcon_argcomplete/hook/colcon-argcomplete.bash
source /usr/share/vcstool-completion/vcs.bash
source /usr/share/colcon_cd/function/colcon_cd.sh
export LIBGL_ALWAYS_SOFTWARE=1
export _colcon_cd_root=~/ros2_ws 
export ROS_DOMAIN_ID=0
export ROS_NAMESPACE=jetson0
export RMW_IMPLEMENTATION=rmw_fastrtps_cpp
export RCUTILS_COLORIZED_OUTPUT=1 
export RCUTILS_LOGGING_USE_STDOUT=0 
export RCUTILS_LOGGING_BUFFERED_STREAM=1
```



