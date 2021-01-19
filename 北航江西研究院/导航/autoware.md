https://www.ncnynl.com/archives/201911/3482.html

```
sudo apt update
sudo apt install -y python-catkin-pkg python-rosdep ros-melodic-catkin
sudo apt install -y python3-pip python3-colcon-common-extensions python3-setuptools python3-vcstool
pip3 install -U setuptools
```


```
git clone https://github.com/CPFL/Autoware.git --recurse-submodules
```

```
cd ~/autoware_ws/src
catkin_init_workspace
cd ../
rosdep install -y --from-paths src --ignore-src --rosdistro melodic
./catkin_make_release -j8
```


```
wget https://autoware-ai.s3.us-east-2.amazonaws.com/sample_moriyama_data.tar.gz

wget https://autoware-ai.s3.us-east-2.amazonaws.com/sample_moriyama_150324.tar.gz
```