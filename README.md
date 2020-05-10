# maplab_ws | Ubuntu 18 | ARM & Intel


## Install of ROS Melodic
http://wiki.ros.org/Installation/Ubuntu

## Install required packages
sudo apt install -y software-properties-common

sudo add-apt-repository "deb http://packages.ros.org/ros/ubuntu bionic main"

wget https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -O - | sudo apt-key add -

sudo apt update

sudo apt install -y ros-melodic-desktop-full doxygen liblapack-dev libblas-dev \

autotools-dev dh-autoreconf libboost-all-dev python-setuptools git g++ cppcheck \

default-jre libgtest-dev libglew-dev clang-format-3.9 python-git \

pylint python-termcolor "ros-melodic-camera-info-manager*" protobuf-compiler protobuf-c-compiler \

python-wstool python-catkin-tools libssh2-1-dev libatlas3-base \

libnlopt-dev ccache ros-melodic-octomap ros-melodic-octomap-ros ros-melodic-gps-common \

"ros-melodic-tf2-*" python-pip python-autopep8 libreadline-dev ifstat ntpdate sysstat libv4l-0

## Update ROS Environment
sudo rosdep init

rosdep update

echo ". /opt/ros/melodic/setup.bash" >> ~/.bashrc

source ~/.bashrc

sudo apt install -y ccache &&\

echo 'export PATH="/usr/lib/ccache:$PATH"' | tee -a ~/.bashrc &&\

source ~/.bashrc && echo $PATH

ccache --max-size=10G


## Clone Repository

export CATKIN_WS=~/maplab_ws

cd ~

git clone --recursive https://github.com/Abdob/maplab_ws

voxblox: 19634c9cb98efececbd8ae63d17e70d4f4594235


initialize the catkin workspace and build project

cd $CATKIN_WS

catkin init

catkin config --merge-devel

catkin config --extend /opt/ros/melodic

catkin config --cmake-args -DCMAKE_BUILD_TYPE=Release

catkin config --cmake-args -DCMAKE_CXX_COMPILER_LAUNCHER=ccache

cd $CATKIN_WS

catkin clean  # Necessary to clean up your workspace as your layout will change.

catkin config --merge-devel

catkin build maplab -j2
