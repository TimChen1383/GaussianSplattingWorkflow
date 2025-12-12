# Gaussian Splatting Workflow (WIP)

## 1. Brief
### 1.1 Concept
This is a very simplified explanation of the Gaussian Splatting concept
- First, locate the camera position > Reconstruct the point cloud > Convert each point into a 3D ellipsoid > Adjust it using AI to achieve the sharpest and most accurate result
- If the video has 300 frames, there are 300 photos taken from slightly different angles
- Render this set of 3D ellipsoids from different angles > Compare them with the original photos > Correct their size, color, position, and transparency, repeating this process continuously
- The 3D ellipsoid is not perfectly round; it is a 3D colored ellipsoid that can be rotated, stretched, and flattened. After the calculation, the shape and size of the ellipsoid are fixed
![3dgs_pipeline_v3-1](https://github.com/user-attachments/assets/bb86f852-0b9a-4c3e-98b7-45d136839ad6)

https://github.com/user-attachments/assets/5d395c7e-6818-4023-919a-0ce1722b0322

### 1.2 Render
- During rendering, all 3D ellipsoids are read > projected onto the screen > and transformed into 2D ellipses on the screen
- The ellipsoids are actually 3D, but because only the view seen by the camera is rendered in 2D, the size and orientation of the ellipsoids will slightly change depending on the camera position
- The final color and transparency are mixed based on the view seen by the camera
- This involves a design with Level of Detail (LOD)
<img width="1526" height="684" alt="forward-splatting" src="https://github.com/user-attachments/assets/109867ba-80e6-460c-bcc4-b88306d9beb2" />

https://github.com/user-attachments/assets/2ffbe27c-db08-44a9-abb2-720cc779c5ff

### 1.3 Data Format
- Opening the .py file directly with Notepad will show the data header:
- Position: X, Y, Z. Position of the GS point
- Color: dc_0, dc_1, dc_2. Color of the GS point
- Opacity: Opacity of the GS point
- Scale: Scale_0, Scale_1, Scale_2. Size of the GS point
- Rotation: rot_0, Rot_1, rot_2, rot_3. Rotation of the GS point
- Different 3D rendering software will read this data
- Later, when discussing rendering, we will show how the data is read in different 3D software.
<img width="828" height="1078" alt="Screenshot 2025-12-09 221231" src="https://github.com/user-attachments/assets/f06e8031-bcab-4f95-8112-e62291d18574" />

## 2. Scanning
### 2.1 Scanning Machine
### 2.2 Scanning Path
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

- Use radar point cloud data to help view current coverage
- The XGrids PortalCam can provide an instant preview of the currently scanned area
<img width="1129" height="715" alt="0 (1)" src="https://github.com/user-attachments/assets/e097dee9-09a6-4b8e-b02d-e6fc0052c310" />

## 3. Generate
### 3.1 Software
- Free and open source
- GitHub link: https://github.com/graphdeco-inria/gaussian-splatting
- Very simple interface
- You need to set up your own environment
<img width="1221" height="717" alt="image (2)" src="https://github.com/user-attachments/assets/23b576ef-84e0-482a-8aea-a33a451c47e9" />

- The company purchased software from the same company that makes Portalcam
- Download link: https://xgrids.com/intl/support/download?page=LCCStudio
- LCC Viewer can convert PLY files to LCC format for use with Unreal Engine's LCC plugin (free)
- LCC Studio can process video to GS, but this requires payment; the company has purchased an account (network required)
<img width="1010" height="626" alt="0 (2)" src="https://github.com/user-attachments/assets/27e700be-de5b-40dd-9169-10e60c8c5caf" />

- Download link: https://www.jawset.com/
- Solving is free, and you can preview the results
- Exporting the solved Jawset will require a paid account
<img width="822" height="580" alt="0 (3)" src="https://github.com/user-attachments/assets/80625a07-3d0d-4cc7-8595-38c07466b18a" />

### 3.2 Generate Process
- Postshot Interface Introduction This tutorial demonstrates how to convert mobile video to GS (Geometry Set) using Postshot.
- Step is the number of training steps, which can be understood as iteratively calculating the color, position, rotation, size, etc., of the GS. You can start with the default 30k setting for calculation. Increasing the number of steps improves the quality of the GS, but also consumes more computer resources and computation time. A balance needs to be struck between quality and computation time (similar to rendering).
- Import the video, set the training steps, and you can start the calculation. It's very simple.
<img width="1760" height="434" alt="Screenshot 2025-12-09 223237" src="https://github.com/user-attachments/assets/7cb6316b-345a-4f77-9181-8dc41eef3c88" />

## 4. Clean up
### 4.1 Software
- LCC Studio (not free)
- SuperSplat (free and open source)
- SuperSplat Web Version: https://superspl.at/editor
- Local Version: https://github.com/playcanvas/supersplat
<img width="1897" height="886" alt="0 (4)" src="https://github.com/user-attachments/assets/df9f04bd-a5ff-4bcb-b9ff-9817b4b51875" />

### 4.2 Clean up
- Most GS editing software is similar in operation. Taking Supersplat as an example
- Common cleanup needs include: Deleting unnecessary points
- Resetting the Pivot Point (the world center is the exported Pivot Point)
- Data after export cleanup
- Cleaning up GS points not visible from the viewpoint can improve rendering performance
<img width="1911" height="875" alt="螢幕擷取畫面 2025-11-24 112948" src="https://github.com/user-attachments/assets/e8b5e232-9621-4730-8abf-2c50cfa8c3a8" />
<img width="1010" height="1079" alt="Screenshot 2025-12-09 224256" src="https://github.com/user-attachments/assets/3cf644b9-2056-4e03-bb08-f423b0bb8c3d" />

## 5. Render
### 5.1 Software
- As mentioned in the previous introduction, the specific file is a PLY file containing special information.
- This information needs to be interpreted and presented within 3D software.
- While the rendering processes of different software are largely similar, some functionalities may vary.
- Blender: KIRI Engine (Geometry Node, extremely poor performance)
<img width="1577" height="395" alt="Geo_Node" src="https://github.com/user-attachments/assets/21a84e28-8127-4f44-bbb5-32d1d72594aa" />

https://github.com/user-attachments/assets/337bdbee-c5db-4c60-8831-46041287f699

- Houdini 21 native support
- The File node reads the PLY file directly, the Bake Splat node interprets it as GS, and Karma renders
- The information of the points can be seen in the Geometry Spreadsheet
<img width="1912" height="1024" alt="0 (5)" src="https://github.com/user-attachments/assets/66926a9c-b173-4d17-b1ef-82a7f49a8581" />

- we usually use Volinga and Xgrids LCC for rendering in Unreal Engine
- Volinga currently offers the best quality, but it requires payment (https://web.volinga.ai/)
- Xgrids LCC (https://developer.xgrids.com/#/download?page=LCC_UNREAL_SDK_UE54)
- LCC Viewer (Free) (https://xgrids.com/intl/support/download?page=LCCViewer)
- Before using the LCC Plugin, you need to convert the PLY file to an LCC file. You can use LCC Viewer for free to convert files. Simply open the PLY file with LCC Viewer, and it will create the LCC file next to it.
- In addition to the LCC file itself, the LCC file contains other files. These files need to be placed in the same folder. When moving to another project, move the entire package.
<img width="1512" height="850" alt="LCC_Viewer" src="https://github.com/user-attachments/assets/52e9e555-56d1-4473-b811-e5e916970942" />

- The following will demonstrate the specific operation of LCC:
- Place the LCC plugin (https://developer.xgrids.com/#/download?page=LCC_UNREAL_SDK_UE54) in the Plugins folder of your UE project
- Add an LCC Actor to your scene
- The LCC actor directly reads the absolute path of the LCC file. It does not need to be imported into the UE project and can exist outside the project
- You can adjust the color, curves, and splat size
<img width="1914" height="1027" alt="LCC" src="https://github.com/user-attachments/assets/cc8b300c-d599-47b7-b9eb-db073f20b0f4" />

- More detailed settings for LCC can be found in the official documentation (https://developer.xgrids.com/#/document?titleId=en-1720509312452)
- Some APIs are available and can be called via BP or C++
<img width="1224" height="878" alt="image (3)" src="https://github.com/user-attachments/assets/64780908-0618-4c94-9454-00bb1459ea42" />
<img width="990" height="552" alt="GS_BPAPI" src="https://github.com/user-attachments/assets/db894488-c4cc-4f71-863a-6e36c039823a" />

### 5.2 Lighting
- Most GS plugins support lighting
- Taking LCC as an example, simply change the Light Mode to Lit
- Color grading and tone mapping are supported
- Currently, using the UE LCC plugin, it's not possible to use GS as an HDRI
- NVIDIA videos appear to have the potential for HDRI use
- Path tracing is not supported
- Checking "Receive Shadow" under LCC Actor allows GS to render object shadows (but noticeable uneven edges in the GS rendering are visible)

https://github.com/user-attachments/assets/49b7a01f-1809-4ad7-bc58-a5f3f1b9e748

https://github.com/user-attachments/assets/0b62ee56-7636-4074-8b43-9bccafab4f30

<img width="1246" height="855" alt="GS_shadow" src="https://github.com/user-attachments/assets/f396a349-f84a-476d-94dd-638d475fd0b2" />


### 5.3 Culling
- You can use the Clipping Volume of the LCC Plugin for culling

https://github.com/user-attachments/assets/89eb8555-b7b4-47d2-917a-b808debfd80e



