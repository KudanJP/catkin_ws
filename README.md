# catkin_ws
3rd party ros drivers

## SDK installation

### Livox SDK2 Installation

```console
cd sdk/Livox-SDK2/
mkdir build
cd build
cmake .. && make -j
sudo make install
```

### RealSense SDK 2.0

```console
sudo mkdir -p /etc/apt/keyrings
curl -sSf https://librealsense.intel.com/Debian/librealsense.pgp | sudo tee /etc/apt/keyrings/librealsense.pgp > /dev/null

echo "deb [signed-by=/etc/apt/keyrings/librealsense.pgp] https://librealsense.intel.com/Debian/apt-repo `lsb_release -cs` main" | \
sudo tee /etc/apt/sources.list.d/librealsense.list
sudo apt-get update

sudo apt-get install librealsense2-dkms -y
sudo apt-get install librealsense2-utils -y
sudo apt-get install librealsense2-dev -y
sudo apt-get install librealsense2-dbg -y
```

## How to build catkin_ws

```console
sudo rosdep init
rosdep update
# rosdep install -i --from-path src --rosdistro $ROS_DISTRO --skip-keys=librealsense2 -y
rosdep install --from-paths src --ignore-src -r -y

# rosbag_fancy
catkin_make --pkg rosbag_fancy_msgs

# Livox MID360
source /opt/ros/noetic/setup.sh
cd catkin_ws/src/livox_ros_driver2
./build.sh ROS1

# Hesai
sudo apt install libpcap-dev libyaml-cpp-dev

# Ouster
sudo apt install -y                     \
    ros-$ROS_DISTRO-pcl-ros             \
    ros-$ROS_DISTRO-rviz
sudo apt install -y         \
    build-essential         \
    libeigen3-dev           \
    libjsoncpp-dev          \
    libspdlog-dev           \
    libcurl4-openssl-dev    \
    cmake                   \
    libflatbuffers-dev

# Realsense
catkin_init_workspace
catkin_make -DCATKIN_ENABLE_TESTING=False -DCMAKE_BUILD_TYPE=Release

catkin_make install
```
