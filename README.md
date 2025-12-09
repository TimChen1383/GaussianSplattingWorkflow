# Gaussian Splatting Workflow

## Brief
### Concept
This is a very simplified explanation of the Gaussian Splatting concept
- First, locate the camera position > Reconstruct the point cloud > Convert each point into a 3D ellipsoid > Adjust it using AI to achieve the sharpest and most accurate result
- If the video has 300 frames, there are 300 photos taken from slightly different angles
- Render this set of 3D ellipsoids from different angles > Compare them with the original photos > Correct their size, color, position, and transparency, repeating this process continuously
- The 3D ellipsoid is not perfectly round; it is a 3D colored ellipsoid that can be rotated, stretched, and flattened. After the calculation, the shape and size of the ellipsoid are fixed
![3dgs_pipeline_v3-1](https://github.com/user-attachments/assets/bb86f852-0b9a-4c3e-98b7-45d136839ad6)

https://github.com/user-attachments/assets/5d395c7e-6818-4023-919a-0ce1722b0322

### Render
- During rendering, all 3D ellipsoids are read > projected onto the screen > and transformed into 2D ellipses on the screen
- The ellipsoids are actually 3D, but because only the view seen by the camera is rendered in 2D, the size and orientation of the ellipsoids will slightly change depending on the camera position
- The final color and transparency are mixed based on the view seen by the camera
- This involves a design with Level of Detail (LOD)
<img width="1526" height="684" alt="forward-splatting" src="https://github.com/user-attachments/assets/109867ba-80e6-460c-bcc4-b88306d9beb2" />

https://github.com/user-attachments/assets/2ffbe27c-db08-44a9-abb2-720cc779c5ff

### Data Format
- Opening the .py file directly with Notepad will show the data header:
- Position: X, Y, Z. Position of the GS point
- Color: dc_0, dc_1, dc_2. Color of the GS point
- Opacity: Opacity of the GS point
- Scale: Scale_0, Scale_1, Scale_2. Size of the GS point
- Rotation: rot_0, Rot_1, rot_2, rot_3. Rotation of the GS point
- Different 3D rendering software will read this data
- Later, when discussing rendering, we will show how the data is read in different 3D software.
<img width="828" height="1078" alt="Screenshot 2025-12-09 221231" src="https://github.com/user-attachments/assets/f06e8031-bcab-4f95-8112-e62291d18574" />

## Scanning
### Scanning Machine
### Scanning Path
- Cover as many viewing angles as possible during scanning
- Scan at different heights. Get close to the object
- Avoid overexposure in the video
- Avoid motion blur in the video
- Adjust machine settings to scan at different heights simultaneously

<img width="1184" height="649" alt="0" src="https://github.com/user-attachments/assets/acd20c6c-0a89-4635-b76d-46f40ef8cccf" />

- Different perspectives seen from a 360 camera
- 360 video split into multiple perspectives
<img width="1246" height="690" alt="特殊360" src="https://github.com/user-attachments/assets/0f1fbf6f-cdd8-459f-81da-250d2ffbaa1d" />
<img width="1189" height="664" alt="image" src="https://github.com/user-attachments/assets/8f8fd4d1-81b1-484b-9e54-c14ea952ec05" />
<img width="1088" height="643" alt="image (1)" src="https://github.com/user-attachments/assets/1d3d2cc6-c008-4357-9ff2-801cce5ca2fb" />

- Approaching the object
- Overlapping routes
- Multiple closed-loop movement lines
<img width="1917" height="386" alt="Screenshot 2025-12-09 222211" src="https://github.com/user-attachments/assets/502dc0fe-c0e4-4612-a92b-25a5d79fa9e6" />
<img width="1719" height="507" alt="Screenshot 2025-12-09 222326" src="https://github.com/user-attachments/assets/e3bb8c12-9dfc-4122-b228-4050e8c86abd" />

