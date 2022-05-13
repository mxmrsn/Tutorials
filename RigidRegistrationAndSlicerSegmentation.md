# Rigid Registration, Meshlab and Slicer Segmentation Tutorial

## Slicer Segmentation
1. Follow and reference Slicer [tutorials](https://slicer.readthedocs.io/en/latest/user_guide/image_segmentation.html) to segment anatomy from CT/MRI 3D dataset. Find example CT scans in the medlab server under /Max/DATA/CTScans/
2. Export the segmentation as STL.

## Meshlab Downsampling
3. Downsample the STL to 30,000 vertices using [Meshlab](https://www.meshlab.net/).
![meshlab_screenshot](/imgs/meshlab_downsample.png)
4. Import STL into Matlab using [stlread()](https://www.mathworks.com/matlabcentral/fileexchange/22409-stl-file-reader)
5. Copy the points of the STL vertices into a variable "pts"
6. Augment the points into homogeneous form ([x y z 1]).
7. Define a known homogeneous transformation matrix to transform the points with.
8. Apply this homogeneous transform to the points by pre-multiplying the points with the transform.
9. Visualize the initial point cloud, and the transformed point cloud.
10. You should now have 2 point clouds, with a known transformation that relates the two. Using the rigid point-based registration algorithm outlined by Fitzpatrick, back out the transform using only the two sets of points.
11. Lastly, 3D print the segmented anatomy on one of the 3D printers.

You are now a Slicer/Rigid Registration Expert!
