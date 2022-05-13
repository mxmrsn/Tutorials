# Rigid Registration, Meshlab and Slicer Segmentation Tutorial

## Slicer Segmentation
1. Follow and reference Slicer [tutorials](https://slicer.readthedocs.io/en/latest/user_guide/image_segmentation.html) to segment anatomy from CT/MRI 3D dataset. Find example CT scans in the medlab server under /Max/DATA/CTScans/
2. Export the segmentation as STL.

## Meshlab Downsampling
3. Downsample the STL to a target of 30,000 faces using [Meshlab](https://www.meshlab.net/). Note that Meshlab can be called from the command line for programmatic deployment/integration with other code. Meshlab is also useful for repairing meshes if they are incomplete or contain holes, need to be smoothed or modified.
![meshlab_screenshot](/imgs/meshlab_downsample.png)

When downsampling the mesh, we have a tradeoff between the amount of detail preserved and the file size. This is a qualitative judgement call. After downsampling the skull mesh, we have:
![downsampled_skull](/imgs/downsampled_skull.png)

Export this stl using "Export Mesh As"

## Matlab Import Mesh
4. Import STL into Matlab using [stlread()](https://www.mathworks.com/matlabcentral/fileexchange/22409-stl-file-reader)
![mesh_matlab](/imgs/mesh_matlab.png)

Using the patch command, we can visualize the stl.
![render_mesh_matlab](/imgs/render_mesh_matlab.png)

## Rigid Registration
5. Copy the points of the STL vertices into a variable "pts"
6. We can visualize the point cloud with the scatter3() command in matlab.
![skull_ptcloud](/imgs/pointcloud_matlab.png)

7. Augment the points into homogeneous form ([x y z 1]).
8. Define a known homogeneous transformation matrix to transform the points with. For example, we can define this transform:
```
 T = [axang2rotm([0 1 0 pi]) [100 -50 -20]'; zeros(1,3) 1];
```

![known_tform](/imgs/known_tform.png)

9. Apply this homogeneous transform to the points by pre-multiplying the points with the transform.
10. Visualize the initial point cloud, and the transformed point cloud.
![tformed_pts](/imgs/tformed_pts.png)

11. You should now have 2 point clouds, with a known transformation that relates the two. Using the rigid point-based registration algorithm outlined by Fitzpatrick, back out the transform using only the two sets of points.
12. Lastly, 3D print the segmented anatomy on one of the 3D printers.

You are now a Slicer/Meshlab/Rigid Registration Expert!
