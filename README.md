# Gaussian Splatting Workflow

## Brief
This is a very simplified explanation of the Gaussian Splatting concept. 
- First, locate the camera position > Reconstruct the point cloud > Convert each point into a 3D ellipsoid > Adjust it using AI to achieve the sharpest and most accurate result.
- If the video has 300 frames, there are 300 photos taken from slightly different angles.
- Render this set of 3D ellipsoids from different angles > Compare them with the original photos > Correct their size, color, position, and transparency, repeating this process continuously.
- The 3D ellipsoid is not perfectly round; it is a 3D colored ellipsoid that can be rotated, stretched, and flattened. After the calculation, the shape and size of the ellipsoid are fixed.
![3dgs_pipeline_v3-1](https://github.com/user-attachments/assets/bb86f852-0b9a-4c3e-98b7-45d136839ad6)
<p align="center" width="100%">
<video src="[https://github.com/user-attachments/assets/563d36e5-1c92-49e6-aa88-c873a20ddf1d](https://github.com/user-attachments/assets/d420a54d-32e7-4729-ae35-a2b01f86f415
)" width="80%" controls></video>
</p>
https://github.com/user-attachments/assets/d420a54d-32e7-4729-ae35-a2b01f86f415

- During rendering, all 3D ellipsoids are read > projected onto the screen > and transformed into 2D ellipses on the screen.
- The ellipsoids are actually 3D, but because only the view seen by the camera is rendered in 2D, the size and orientation of the ellipsoids will slightly change depending on the camera position.
- The final color and transparency are mixed based on the view seen by the camera.
- This involves a design with Level of Detail (LOD).
<img width="1526" height="684" alt="forward-splatting" src="https://github.com/user-attachments/assets/109867ba-80e6-460c-bcc4-b88306d9beb2" />
https://github.com/user-attachments/assets/65ade23d-9873-4c83-ae58-6f7223f8fc65

