---
title: Frustum PointNet with Geometry features
layout: post
tags: U.C.Berkeley
img: frustum.jpg
categories: ''
---
3D object detection is a popular topic for autonomous driving. Most methods for 3D object detection is based on LIDAR information, while Frustum PointNets is a novel method to combine LIDAR and image information for de-tection. Currently, most 3D object detection algorithms take raw point cloud as input without any preprocessing. It’s often overlooked how the 3D structure of point cloud may help for 3D instance segmentation and detection. 

In our work, we study how geometry features from point cloud can improve the 3D object detection. We find that the geometry features from point cloud can improve the detec-tion of all the classes. Evaluated on KITTI 3D detection benchmarks, our method gains as large as __6.06%__ more accuracy than the original method.

## Geometry Feature Counts
In our proposed method, we learn the geometry features of point cloud, such as normal, linearity and curvature. Then we add them as new channels in Frustum PointNets and see improvement.
![Normal]({{site.baseurl}}/assets/img/normal.png)

## Method
The goal is to concatenate geometry features into Frustum PointNets. The first step is to generate different kinds of geometry features, such as normal and covariance features. Then, adding them as new channels in PointNets for better 3D semantic segmentation and 3D bounding box estimation.
![Framework]({{site.baseurl}}/assets/img/framework_f.png)

## Result
 After applying our adaptive method to compute the normal, it shows that the results for all of the classes improve, while for cyclist detection the result is not as good as radius fixed as 3m, which demonstrates that overall the optimal radius is needed to attain more appropriate geometry features.

![Result]({{site.baseurl}}/assets/img/result.png)