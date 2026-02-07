# GLIM to HDMapping simlified instruction

## Step 1 (prepare data)
Download the dataset `reg-1.bag` by clicking [link](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) (it is part of [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset)) and convert with [tool](https://github.com/MapsHD/livox_bag_aggregate) to 'reg-1.bag-pc.bag'.

File 'reg-1.bag-pc.bag' is an input for further calculations.
It should be located in '~/hdmapping-benchmark/data'.

We now convert data from ROS1 to ROS2

```shell
docker run -it -v ~/hdmapping-benchmark/data:/data --user 1000:1000 glim_humble /bin/bash
cd /data
rosbags-convert --src reg-1.bag-pc.bag --dst reg-1-ros2 
```

close terminal

## Step 2 (prepare docker)

open new terminal

```shell
mkdir -p ~/hdmapping-benchmark
cd ~/hdmapping-benchmark
git clone https://github.com/MapsHD/benchmark-GLIM-to-HDMapping.git --recursive
cd benchmark-GLIM-to-HDMapping
git checkout Bunker-DVI-Dataset-reg-1
docker build -t glim_humble .
```

## Step 3 (run docker, file 'reg-1-ros2' should be in '~/hdmapping-benchmark/data')
```shell
cd ~/hdmapping-benchmark/benchmark-GLIM-to-HDMapping
chmod +x docker_session_run-ros2-glim.sh 
cd ~/hdmapping-benchmark/data
~/hdmapping-benchmark/benchmark-GLIM-to-HDMapping/docker_session_run-ros2-glim.sh reg-1-ros2 .
```

## Step 4 (Open and visualize data)
Expected data should appear in ~/hdmapping-benchmark/data/output_hdmapping-glim
Use tool [multi_view_tls_registration_step_2](https://github.com/MapsHD/HDMapping) to open session.json from ~/hdmapping-benchmark/data/output_hdmapping-glim.

You should see following data

lio_initial_poses.reg

poses.reg

scan_lio_0.laz

scan_lio_1.laz

scan_lio_2.laz

scan_lio_3.laz

scan_lio_4.laz

scan_lio_5.laz

scan_lio_6.laz

scan_lio_7.laz

scan_lio_8.laz

scan_lio_9.laz

session.json

trajectory_lio_0.csv

trajectory_lio_1.csv

trajectory_lio_2.csv

trajectory_lio_3.csv

trajectory_lio_4.csv

trajectory_lio_5.csv

trajectory_lio_6.csv

trajectory_lio_7.csv

trajectory_lio_8.csv

trajectory_lio_9.csv

## Contact email
januszbedkowski@gmail.com