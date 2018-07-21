# Pointcloud Tutorial

The purpose of this tutorial is to provide examples of how to work with 3D or multidimensional data using two popular libraries: Point Cloud Library (PCL) and Open3D.
These examples will cover such topics as I/O, features, keypoints, registration, segmentation, and sample consensus.

## Preliminaries and Dependencies
Your system should have a modern compiler that supports C++11, as well as git and CMake. To use the python bindings for Open3D, you will also need either python 2.7 or 3.5+.

### PCL
If you have ROS installed already, then you should have a version of PCL on your computer already.  
If not, then you can install pre-built binaries (or build from source) for a variety of operating systems based on these instructions: [http://www.pointclouds.org/downloads/](http://www.pointclouds.org/downloads/).
The Ubuntu directions are copied below for convenience:
```
sudo add-apt-repository ppa:v-launchpad-jochen-sprickerhof-de/pcl
sudo apt-get update
sudo apt-get install libpcl-all
```
Even if you have a version of the library through ROS, you should also install some tools for interfacing with the library in a non-ROS way:
```
sudo apt-get install pcl-tools
```

### Open3D
This library can be installed from source, according to these directions [http://www.open3d.org/docs/getting_started.html#ubuntu](http://www.open3d.org/docs/getting_started.html#ubuntu).
First, get the code:
```
git clone https://github.com/IntelVCL/Open3D
```
and then follow the directions for your OS.

### Building the Examples
1. If you're reading this README, you've probably already cloned this repository, but if not,
navigate to your desired install directory and run:
```
git clone git@github.com:jeffdelmerico/pointcloud_tutorial.git
```

2. Navigate into the pointcloud_tutorials directory, then execute the following commands to build the
examples:
```
mkdir build
cd build
cmake ..  
make -j8 && make install
```

3. Assuming the examples all built correctly, you should have some executables in a new `bin` directory.

## Running the Examples
```
cd ../bin
```
### I/O:
#### PCL
    - write a pcd file of randomly generated points and visualize it with pcd_viewer
        ./pcl_write_pcd
        pcl_viewer test_pcd.pcd
    - read in that same pcd file
        ./pcl_read_pcd
    - grab point clouds from an RGBD camera (be sure one is connected)
        ./pcl_openni_grabber
#### Open3D

### 3D Features:
#### PCL
    - compute point normals on a point cloud and use built-in visualizer
        ./pcl_compute_normals
#### Open3D

### Filtering:
#### PCL    
    - run one of 3 different filters on a point cloud
        ./pcl_filtering 0  (pass through filter)
        ./pcl_filtering 1  (downsample to a voxel grid)
        ./pcl_filtering 2  (perform statistical outlier removal)
    - visualize the output side-by-side with the original
        pcl_viewer -multiview 1 ../data/table_scene_lms400.pcd table_scene_lms400_filtered.pcd
      press 'r' to zero the viewpoint, and 'l' to list the color handlers
#### Open3D

### Keypoints:
#### PCL
    - Find SIFT keypoints in a point cloud and visualize
        ./pcl_keypoints ../data/robot1.pcd keypoints
    - Compute PFH features on SIFT keypoints for two point clouds and then compute their
      correspondences
        ./pcl_keypoints ../data/robot correspondences
#### Open3D

### Trees:
#### PCL
    - Put some random points into a KdTree; do NN and radius search near a random point in space
        ./pcl_kdtree
    - Put some random points into an Octree; do voxel, NN, and radius search near a random point in
      space
        ./pcl_octree
#### Open3D

### Sample Consensus:
#### PCL
    - Generate some points that fit a planar model as well as a bunch of outliers
        ./pcl_sample_consensus
    - Generate points as before, but use sample consensus to find inliers to a planar model
        ./pcl_sample_consensus -f
#### Open3D

### Segmentation:
#### PCL
    - Perform iterative plane segmentation on real point cloud data
        ./pcl_plane_segmentation
    - Visualize the output side-by-side with the original
        pcl_viewer -multiview 1 ../data/table_scene_lms400.pcd table_scene_lms400_first_plane.pcd table_scene_lms400_second_plane.pcd
    - Perform euclidean cluster extraction after removing the dominant planes in the scene
        ./pcl_euclidean_cluster_extraction
    - Visualize the output with all clusters in the same viewport
        pcl_viewer cloud_cluster_0.pcd cloud_cluster_1.pcd cloud_cluster_2.pcd cloud_cluster_3.pcd cloud_cluster_4.pcd
#### Open3D

### Registration:
#### PCL
    - Perform iterative closest point to align two point clouds
        ./pcl_icp ../data/robot1.pcd ../data/robot2.pcd
    - Visualize aligned and combined point cloud beside originals
        pcl_viewer -multiview 1 ../data/robot1.pcd ../data/robot2.pcd icp_aligned.pcd
    - Attempt to fit several point cloud templates to the target point cloud, output the best match
        ./pcl_template_matching ../data/object_templates.txt ../data/person.pcd
    - Visualize the matched and aligned template against the target PC
        pcl_viewer ../data/person.pcd template_aligned.pcd
      you may need to press '1' several times to get a good color scheme for the two point clouds
      to be visible
#### Open3D


## More Tutorials
Some of the PCL examples here were adapted from these tutorials: [http://www.pointclouds.org/documentation/tutorials/](http://www.pointclouds.org/documentation/tutorials/), but there are many more topics covered there.
The Open3D examples were also adapted from the official tutorials [http://www.open3d.org/docs/tutorial/index.html](http://www.open3d.org/docs/tutorial/index.html) where there are further examples.
