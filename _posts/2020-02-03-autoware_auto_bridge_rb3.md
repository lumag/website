---
title: "96boards: Autoware everywhere | Autoware.Auto, bridge with .AI and Dragonboard-845c"
author: Servando German Serrano
date: 2020-02-03 01:00:00+00:00
image: /assets/images/blog/awf_db845.png
image_name: awf_db845.png
categories: blog
series: "96boards: Autoware everywhere"
tags: 64-bit, 96Boards, aarch64, ARM, ARMv8, Consumer Edition, dragonboard-845c, rb3, Linaro, Linux, arm64, real time, ROS2, Autoware
---

# Introduction

In our previous [entry](https://www.96boards.org/blog/autoware.ai_rb3/) we showed how to get Autoware.AI running on the [Qualcomm® Robotics (RB3) Dragonboard-845c Development Platform](https://www.96boards.org/product/rb3-platform/). In this post we will look at Autoware.Auto and how to bridge Autoware.AI and Autoware.Auto in the same way as we did for the Hikey970.

The post is organized as follows:
- [Requirements](#requirements)
- [Getting the Docker images](#getting-the-docker-images)
- [Getting the demo data](#getting-the-demo-data)
- [Running the demos](#running-the-demos)
  - [.Auto 3D Perception demo](#auto-3d-perception-demo)
  - [.AI and .Auto bridge](#ai-and-auto-bridge)
    - [.AI terminals](#ai-terminals)
    - [ros1_bridge terminal](#ros1_bridge-terminal)
    - [.Auto terminals](#auto-terminals)
    - [Stopping the mapping process](#stopping-the-mapping-process)
    - [Visualizing the pointcloud map](#visualizing-the-pointcloud-map)

***

## Requirements

The steps outlined in this blog posts build on our previous posts and as such you need to:
- Have your RB3 board running with Debian Buster as outlined [here](https://www.96boards.org/product/rb3-platform/) and with [Docker installed.](https://www.96boards.org/blog/db845-ros2/#installing-docker)
- Be familiar with the work that we conducted previously within the "Autoware everywhere" series on [Autoware.Auto](https://www.96boards.org/blog/autoware.auto_hikey970/) and [how to bridge both](https://www.96boards.org/blog/autoware_bridge_hikey970/) on the Hikey970.

In addition, if you plan on developing real-time applications in the future your board should be running a RT-enabled kernel as we outlined [here](https://www.96boards.org/blog/db845-rt/).

For visualization purposes we will also use a separate laptop, where we need to have ROS2 available.

## Getting the Docker images

We need to get the following Docker images:

```
$ docker pull 96boards/autoware:auto_20200121
$ docker pull 96boards/ros:ros1_bridge
```

## Getting the demo data

In addition to the Docker images we need to get the demo data for the [Autoware.Auto 3D Perception Stack demo](https://autowarefoundation.gitlab.io/autoware.auto/AutowareAuto/perception-stack.html). To do so:

- Move into the `shared_dir` folder that we created as part of the previous post and download the demo data and parameters file:

```
$ cd ~/shared_dir
$ wget http://people.linaro.org/~servando.german.serrano/autoware/autoware.auto_get_demo_data
$ chmod +x autoware.auto_get_demo_data
$ ./autoware.auto_get_demo_data
$ wget http://people.linaro.org/~servando.german.serrano/autoware/vlp16_test.param_ai.yaml
```

## Running the demos

We are now set to start with the different demos. Let's find out how far we can push the RB3 board.

### .Auto 3D Perception demo

To run the Autoware.Auto 3D Perception Stack demo we will roughly follow the steps [here](https://autowarefoundation.gitlab.io/autoware.auto/AutowareAuto/perception-stack.html) but adapted to our setup.

In the laptop we get the config files and open 2 terminals to run 2 instances of `rviz2` as:

```
$ wget https://gitlab.com/autowarefoundation/autoware.auto/AutowareAuto/raw/master/src/tools/autoware_auto_examples/rviz2/autoware.rviz
$ wget https://gitlab.com/autowarefoundation/autoware.auto/AutowareAuto/raw/master/src/tools/autoware_auto_examples/rviz2/autoware_voxel.rviz
```

- Laptop: _Terminal 1_:

```
$ rviz2 -d autoware.rviz
```

- Laptop: _Terminal 2_:

```
$ rviz2 -d autoware_voxel.rviz
```

Now we need to `ssh` into the RB3 in **4** terminals and do the following:

- In _Terminal 1_:

```
$ docker run -it --rm --privileged --net=host -u linaro -v ~/shared_dir:/home/linaro/shared_dir:rw 96boards/autoware:auto_20200121 /bin/bash
$ cd ~
$ source AutowareAuto/install/setup.bash
```

- In terminals 2 to 4 we need to access the running container as we did [here](https://www.96boards.org/blog/autoware.ai_rb3/#running-the-ai-rosbag-demo) but using the `linaro` user:

```
$ docker exec -it -u linaro CONTAINER_NAME /bin/bash
$ cd ~
$ source AutowareAuto/install/setup.bash
```

And then:

- RB3: _Terminal 1_:

```
$ udpreplay ~/shared_dir/route_small_loop_rw-127.0.0.1.pcap
```

- RB3: _Terminal 2_:

```
$ ros2 run velodyne_node velodyne_cloud_node_exe __params:=/home/"${USER}"/AutowareAuto/src/drivers/velodyne_node/param/vlp16_test.param.yaml
```

- RB3: _Terminal 3_:

```
$ ros2 run ray_ground_classifier_nodes ray_ground_classifier_cloud_node_exe __params:=/home/"${USER}"/AutowareAuto/src/perception/filters/ray_ground_classifier_nodes/param/vlp16_lexus.param.yaml
```

- RB3: _Terminal 4_:

```
$ ros2 run voxel_grid_nodes voxel_grid_cloud_node_exe __params:=/home/"${USER}"/AutowareAuto/src/perception/filters/voxel_grid_nodes/param/vlp16_lexus_centroid.param.yaml
```

If everything went fine we will be able to visualize the demo point cloud and downsampled one in the running `rviz2` GUIs as can be seen in the image below.

![](/assets/images/blog/autoware_auto_rb3.png)

### .AI and .Auto bridge

We will now replicate the steps that were outlined [here](https://www.96boards.org/blog/autoware_bridge_hikey970/) for the Hikey970. Hence, for a full description of the steps please follow that blog post.

As we did for the Hikey970, we will use **5** terminals in the RB3, terminals 1 and 2 for the .AI container, terminal 3 for the ros1_bridge container and 4 and 5 for the .Auto container.

#### .AI terminals

- Terminal 1

```
$ cd docker/generic
$ ./run.sh -c off -i autoware/arm64v8 -t 1.13.0
$ mkdir ~/.autoware
$ cp -r ~/shared_dir/data ~/.autoware/data
$ roscore &
$ rosparam load ~/shared_dir/headless_setup.yaml &
$ roslaunch lidar_localizer ndt_mapping.launch
```

- Terminal 2

```
$ docker exec -it -u autoware CONTAINER_NAME /bin/bash
$ cd ~
$ source Autoware/install/setup.bash
```

#### ros1_bridge terminal

- Terminal 3

```
$ docker run -it --rm --privileged --net=host -u linaro 96boards/ros:ros1_bridge /bin/bash -c "source /opt/ros/melodic/setup.bash && source /opt/ros/dashing/local_setup.bash && ros2 run ros1_bridge dynamic_bridge --bridge-all-topics"
```

#### .Auto terminals

- Terminal 4

```
$ docker run -it --rm --privileged --net=host -u linaro -v ~/shared_dir:/home/linaro/shared_dir:rw 96boards/autoware:auto_20200121 /bin/bash
$ source AutowareAuto/install/setup.bash
$ ros2 run velodyne_node velodyne_cloud_node_exe __params:=/home/"${USER}"/shared_dir/vlp16_test.param_ai.yaml
```

- Terminal 5

```
$ docker exec -it -u linaro CONTAINER_NAME /bin/bash
$ source AutowareAuto/install/setup.bash
$ udpreplay ~/shared_dir/route_small_loop_rw-127.0.0.1.pcap
```

A typical look of the terminals running the different nodes is shown in the image below.
![](/assets/images/blog/autoware_bridge_rb3.png)

#### Stopping the mapping process

The computational needs for the mapping task are quite heavy and so the processing will take longer as the number of points in the map grows. We can stop the pcap replaying by doing `Ctrl+C` in terminal 5. To save the map, in terminal 2 we do:

```
$ rostopic pub /config/ndt_mapping_output autoware_config_msgs/ConfigNDTMappingOutput "header:
  seq: 0
  stamp:
    secs: 0
    nsecs: 0
  frame_id: 'map'
filename: 'auto_map.pcd'
filter_res: 0.2"
```

Once the mapping process is complete the `pcd` map will be generated in the `.ros` folder. We need to move it to `shared_dir` if we want to keep it after we stop the container.

```
$ mv ~/.ros/auto_map.pcd ~/shared_dir/
```

![](/assets/images/blog/autoware_bridge_map_save_rb3.png)

#### Visualizing the pointcloud map

To visualize the pointcloud map we need to:
- `scp` the `pcd` from the RB3 to the laptop and store it in `shared_dir`.
- Start an Autoware.AI container as we did [here](https://www.96boards.org/blog/autoware.ai_hikey970/#in-laptop).

```
$ cd ~/docker/generic
$ ./run.sh -c off -t 1.13.0
$ cd shared_dir
$ roscore &
$ rosrun map_file points_map_loader noupdate `pwd`/auto_map.pcd &
$ rviz
```

Within `rviz` we can select the `/points_map` topic and, as we did previously, increase the `Size` to 0.1. The result is displayed below.

![](/assets/images/blog/autoware_bridge_map_rb3.png)

***

# Conclusion

With this post we now have 2 different boards ([Hikey970](https://www.96boards.org/product/hikey970/) and [Qualcomm® Robotics (RB3) Dragonboard-845c Development Platform](https://www.96boards.org/product/rb3-platform/)) that we can use for development of Autoware.
