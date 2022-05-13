# Rigid Registration, Meshlab and Slicer Segmentation Tutorial

## Slicer Segmentation
1. Follow and reference Slicer [tutorials](https://slicer.readthedocs.io/en/latest/user_guide/image_segmentation.html) to segment anatomy from CT/MRI 3D dataset. Find example CT scans in the medlab server under /Max/DATA/CTScans/
2. Export the segmentation as STL. Make sure that the coordinates are defined in the RAS coordinates, otherwise LPS is a left-handed coordinate system and you have to manually flip a dimension to make it proper.

## Meshlab Downsampling
3. Downsample the STL to a target of 30,000 faces using [Meshlab](https://www.meshlab.net/). Note that Meshlab can be called from the command line for programmatic deployment/integration with other code. Meshlab is also useful for repairing meshes if they are incomplete or contain holes, need to be smoothed or modified.

![meshlab_screenshot](/imgs/reg_tut/meshlab_downsample.png)

When downsampling the mesh, we have a tradeoff between the amount of detail preserved and the file size. This is a qualitative judgement call. After downsampling the skull mesh, we have:

![downsampled_skull](/imgs/reg_tut/downsampled_skull.png)

Export this stl using "File >> Export Mesh As"

## Matlab Import Mesh
4. Import STL into Matlab using [stlread()](https://www.mathworks.com/matlabcentral/fileexchange/22409-stl-file-reader)

![mesh_matlab](/imgs/reg_tut/mesh_matlab.png)

Using the patch command, we can visualize the stl. The patch command takes a bunch of key-value pairs, but we only need to set 'Faces', 'Vertices', and some coloring options:
```
patch('Faces',M.faces,'Vertices',M.vertices,'EdgeColor','none','FaceColor','r')
daspect([1 1 1]); view(3); camlight headlight;
```

The ```daspect([1 1 1])``` command sets the aspect ratio of the view to make sure everything is 1:1. The camlight provides some reflections that makes the mesh look nicer.

![render_mesh_matlab](/imgs/reg_tut/render_mesh_matlab.png)

## Rigid Registration
5. Copy the points of the STL vertices into a variable "pts"
6. We can visualize the point cloud with the scatter3() command in matlab.

![skull_ptcloud](/imgs/reg_tut/pointcloud_matlab.png)

7. Augment the points into homogeneous form ([x y z 1]).
8. Define a known homogeneous transformation matrix to transform the points with. For example, we can define a transform that rotates 180 about the y-axis and then translates some arbitrary offset:
```
 T = [axang2rotm([0 1 0 pi]) [100 -50 -20]'; zeros(1,3) 1];
```

![known_tform](/imgs/reg_tut/known_tform.png)

9. Apply this homogeneous transform to the points by pre-multiplying the points with the transform.
10. Visualize the initial point cloud, and the transformed point cloud.

![tformed_pts](/imgs/reg_tut/tformed_pts.png)

11. You should now have 2 point clouds, with a known transformation that relates the two. Using the rigid point-based registration algorithm outlined by Fitzpatrick, back out the transform using only the two sets of points. Note that this approach assumes that we know the point correspondence (i.e. if we were to label all of the points in the pointcloud from 1-90,000, we know the point number in each of the meshes). This is often not the case. If we do not know point correspondences, we can solve for them using ICP, where we solve for a correspondence matrix C and the rigid transform T that relates the two point clouds.

Rigid Point-Based Registration Solves:

$ \min_{T \in SE(3)} \sum_{i=1}^{N} \hspace{1mm} \rVert Tp^{m_i} - p^{s_i} \lVert^2$

Iterative Closest Point (ICP) Registration Solves:

$ \min_{T \in SE(3), C} \sum_{i=1}^{N_s} \sum_{j=1}^{N_m} C_{ij} \hspace{1mm} \lVert Tp^{m_j} - p^{s_i} \rVert^2 $

12. Lastly, 3D print the segmented anatomy on one of the 3D printers.

You are now a Slicer/Meshlab/Rigid Registration Expert!
