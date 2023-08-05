# 3D-to-2D-Projections-and-Rotation-Visualization

This project focuses on visualizing 3D object projection and rotation using MATLAB. The code provides implementations of perspective and weak perspective projections, as well as object rotation around the z-axis. The resulting projections are compared and visualized to showcase the effects of these transformations.

## Introduction

In computer graphics and computer vision, understanding how 3D objects are projected onto a 2D plane and how they can be transformed through rotation is fundamental. This project aims to provide a practical demonstration of these concepts using MATLAB. By exploring various projection techniques and rotation transformations, users can gain insights into the principles that underlie image rendering and manipulation.

## Implementation

The project is implemented using MATLAB and is structured as follows:

1. **Coordinate Points and Projection Functions:**
   - `perspective`: Implements perspective projection for a given set of points.
   - `weak_perspective`: Implements weak perspective projection for a set of points.

2. **Visualization Functions:**
   - `plotting`: Plots original and projected coordinates for comparison.
   - `plot_object`: Visualizes original and rotated objects along with their projections.
   - `rotated_plot`: Compares original and rotated projections.

3. **Rotation and SSD Calculation:**
   - `rotation`: Rotates a set of points around the z-axis by a specified angle.
   - `ssd`: Computes the Sum of Squared Differences between two sets of points.

4. **Main Script (`main_script.m`):**
   - Defines coordinate points, focal length, and rotation angle.
   - Calculates perspective and weak perspective projections.
   - Performs object rotation and calculates rotated projections.
   - Displays results and SSD values.
  
Certainly! Here's a step-by-step guide on how to implement and run the program:

### Step 1: Install MATLAB
Ensure you have MATLAB installed on your system. If you don't have MATLAB, you can download and install it from the [official MathWorks website](https://www.mathworks.com/products/matlab.html).

### Step 2: Create a New Folder
Create a new folder for your project. This will be the directory where you'll save your MATLAB script and functions.

### Step 3: Write the MATLAB Code

1. **Create a new MATLAB script (`main_script.m`):**
   Open a text editor and create a new file named `main_script.m` within your project folder.

2. **Copy and Paste the Code:**

3. **Modify Parameters (Optional):**
   Modify the coordinate points, focal length, rotation angle, or any other parameters according to your requirements. These modifications can be made directly in the `main_script.m` file.

### Step 4: Save and Run the Script

1. **Save the Script:**
   Save the `main_script.m` file in your project folder.

2. **Open MATLAB:**
   Open MATLAB on your computer.

3. **Navigate to the Project Folder:**
   In MATLAB, navigate to the directory where you saved your `main_script.m` file using the `cd` command. For example:
   ```matlab
   cd 'path/to/your/project/folder'
   ```

4. **Run the Script:**
   Type the name of the script (without the `.m` extension) and press Enter to run it:
   ```matlab
   main_script
   ```

### Step 5: Interpret the Results

After running the script, you should see various plots and outputs in the MATLAB environment. These visualizations and results will help you understand the effects of perspective projections, weak perspective projections, and object rotation on 3D objects.

### Step 6: Experiment and Upgrade (Optional)

If you want to experiment with different parameters, such as coordinate points, focal length, or rotation angles, you can modify the values in the `main_script.m` file and rerun the script. Additionally, if you wish to upgrade the project by adding more features or refining the visualizations, you can edit the functions or add new ones accordingly.

Remember that MATLAB is an interactive environment, so you can experiment, modify, and rerun the code as needed to explore different scenarios and visualize the effects of various transformations.

## Certainly! Below is a comprehensive explanation of each part of the code, including its purpose and functionality:

```matlab
clear; clc; close all;
```
These lines clear the workspace, and command window, and close all open figures before executing the rest of the code.

```matlab
Points = [-1, 0, 2; 1, 0, 5; 0, 1, 4; 0, -1, 3];
focal_length = 1;
```
Here, we define a 4x3 matrix `Points`, where each row represents a 3D point with its x, y, and z coordinates. The `focal_length` is set to 1, representing the focal length of the camera.

```matlab
function Pers_Projection = perspective(Points, focal_length)
    Z = Points(:, 3);
    Pers_Projection = bsxfun(@times, Points(:, 1:2), focal_length ./ Z);
end
```
The function `perspective` calculates the perspective projection of the 3D points onto a 2D plane. It takes `Points` and `focal_length` as inputs and returns `Pers_Projection`, which contains the projected 2D points. The function first extracts the z-coordinates of the points and then calculates the projected x and y coordinates using the focal length and z-coordinates.

```matlab
function WPers_Projection = weak_perspective(Points, focal_length)
    Z0 = mean(Points(:, 3));
    WPers_Projection = bsxfun(@times, Points(:, 1:2), focal_length ./ Z0);
end
```
The function `weak_perspective` computes the weak perspective projection of the 3D points onto a 2D plane. It takes `Points` and `focal_length` as inputs and returns `WPers_Projection`, which contains the weak perspective projections. The function first calculates the mean z-coordinate, `Z0`, of all the points and then uses it to compute the projected x and y coordinates.

```matlab
function plotting(Points, Pers_Projection, WPers_Projection)
    figure;
    subplot(1, 4, [1 3]);
    % Plot 3D points and their perspective and weak perspective projections.
    % Add camera marker.
    % Set axis limits, labels, and grid.
    
    subplot(1, 4, 4);
    % Plot 2D projections of points.
    % Add camera marker.
    % Set title and legend.
end
```
The function `plotting` creates a figure with subplots. In the first subplot (3x1 grid), it visualizes the 3D points (`Points`) and their perspective projections (`Pers_Projection`) and weak perspective projections (`WPers_Projection`). The camera position is marked with a marker in all the plots. The axis limits, labels, and grid are set to enhance visualization.

In the second subplot (1x1 grid), it plots the 2D projections of the points (`Points(:, 1:2)`), their perspective projections (`Pers_Projection(:, 1:2)`), and weak perspective projections (`WPers_Projection(:, 1:2)`). The camera marker is also added to this subplot, and a title and legend are set for clarity.

```matlab
function Rotate_Projection = rotation(theta, Points)
    Rz = [cosd(theta) -sind(theta) 0; sind(theta) cosd(theta) 0; 0 0 1];
    Rotate_Projection = (Rz * Points')';
end
```
The function `rotation` performs a rotation of the 3D points (`Points`) around the z-axis by the angle `theta` (in degrees). It takes `theta` and `Points` as inputs and returns `Rotate_Projection`, which contains the rotated 3D points. The function calculates a 3x3 rotation matrix `Rz` for the given angle `theta` and applies this rotation to the points using matrix multiplication.

```matlab
function A = ssd(Pers_Projection, WPers_Projection)
    A = sum(sum(abs(Pers_Projection - WPers_Projection).^2));
end
```
The function `ssd` calculates the Sum of Squared Differences (SSD) between two sets of projected points, `Pers_Projection` and `WPers_Projection`. It returns `A`, which represents the SSD between the two sets. The SSD is calculated as the squared absolute differences between corresponding elements of the two matrices and then summed.

The subsequent sections of the code use the defined functions to perform various tasks, including calculations, visualizations, and comparisons of the original and transformed 3D objects and their projections. The provided comments in the code indicate the specific steps taken in each section.

Please note that this code is designed to work within the MATLAB environment, and the functions provided should be used in conjunction with each other to achieve the desired visualization and analysis of 3D object projection and rotation.

## Upgrading the Project

This project can be extended and improved in various ways:
- Implement additional projection methods (e.g., orthographic projection).
- Explore other rotation axes and angles to visualize different transformations.
- Enhance visualization by incorporating interactive controls.
- Integrate 3D object modeling techniques to create custom shapes.
- Develop a user-friendly GUI for parameter input and visualization control.

Contributions to enhance, optimize, and expand the project are highly encouraged.
