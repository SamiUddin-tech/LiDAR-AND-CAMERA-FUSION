# LiDAR_Camera_Fusion

In this Project, I practiced some most advanced skills that Self Driving Car Engineers use to fuse LiDARs with Cameras.
LiDAR is used more and more in almost every robotics startup, and merging it with a camera is really cool!

**Note:** There is no such a thing like *self driving car engineer*. There are *Perception Engineers*, *Sensor Fusion Engineers*, *Control Engineers* and so on.

## Three Most Important things about Sensor Fusion
In this Project, I have built my understanding around three most important things about *Sensor Fusion*:
1. Sensors and Sensor Fusion
2. Early Fusion
3. Late Fusion

## 1. Sensors and  Sensor Fusion
In this project, my focus is on Cameras and LiDARs (IMAGES and POINT CLOUDS), which are being used by almost every Self Driving Car Company.

### Cameras:
Today, Cameras are very scalable and integrated in every Self Driving Car.

![image](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/373d00c9-d679-4543-bf05-33cf695bbd31)
In above Picture, which is taken from [here](https://electrek.co/2016/10/20/tesla-new-autopilot-hardware-suite-camera-nvidia-tesla-vision/), it's the [Tesla](https://www.tesla.com/)'s Autopilot. And notice that we have 3 cameras, one in left, one in right and one in the center, side cameras are generally called stereo pairs which makes it easy to estimate disance to an obstacle.

Another example of my OpenCV AI Kit with Depth [OAK-D](https://shop.luxonis.com/products/oak-d), Stereo Camera, which is architectured by [Brandon Gilles](https://www.linkedin.com/in/brandon-gilles-5400b734/) (Late) Founder of [LUXONIS](https://www.luxonis.com/) Robotic Vision Startup. Just notice the Object Detection and Depth Perception (X,Y,Z), we get with [OAK-D](https://shop.luxonis.com/products/oak-d).

### LiDARs:
LiDAR (Light Detection and Ranging)

![image](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/98a2bdb2-c2e3-45a0-9072-f77b27aecff8)

In above picture, which is taken from [here](https://www.businessinsider.com/how-does-googles-waymo-self-driving-car-work-graphic-2017-1), it's the [waymo](https://waymo.com/)'s autonomous vehicle. 

So, This is how LiDAR sensors work:

![lidar_working](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/95ea83b8-9f84-4520-ad23-dcb538bf7fd5)

1. They send out a beam of light.
2. This light beam hits an object and bounces back.
3. LiDAR measures how long it takes for the light to bounce back.
4. Using the time it takes (time-of-flight), LiDAR calculates the distance to the object.

So, LiDAR uses the time it takes for light to hit something and come back to figure out how far away that thing is. This helps create detailed maps of the surroundings and is used in technologies like autonomous cars and mapping.
Above Picture is taken from [here](https://www.mathworks.com/help/lidar/ug/lidar-processing-overview.html)

### Point Clouds:

LiDAR generate point clouds. Point clouds are collections of points, and each point has its XYZ position. This allows us to accurately know the depth and distance of every obstacle or object in a 3D space.

Let's take a look at the following video to understand more about Point Clouds, I captured these point clouds with [Basler Blaze 101 Time of Flight Camera](https://www.baslerweb.com/en/products/cameras/3d-cameras/basler-blaze/blaze-101/). To know more about this check my project Safe Rail.

### Camera and LiDAR Fusion:

A self-driving car typically has:

**Multiple Cameras:** These cameras have different angles and capabilities. Some can see far with a narrow view, while others have a wider view but shorter range.

**LiDARs:** These sensors detect objects around the car and precisely estimate their 3D positions.

### Sensor Fusion:

## 2. Early Fusion

To do early fusion I performed three steps:

1. Project the Point Clouds (3D) to the Image(2D)
2. Detect Obstacles in 2D (Camera)
3. Fuse the Results

### 1. Projecting a Point Cloud to an Image

So, here is the Self Driving Car Setup from [KITTI Vision Benchmark Suite](https://www.cvlibs.net/datasets/kitti/setup.php), It works well for learning sensor Fusion.


This Self Driving Car setup has one Valodyne LiDAR (HDL-64E Laser Scanner), and a total of 4 cameras, 2 color cameras and 2 Grayscale cameras, Two cameras (Color and Gray) on left side, two cameras (Color and Gray) on right side. The sensors orientation is not the same, coordinate system is different and psition is also different. https://velodynelidar.com/blog/hdl-64e-lidar-sensor-retires/

**Projecting a LiDAR Point (3D) in a Camera Image (2D)**

Considering an image, and a point cloud, and this is the output of projection!


And to do this projection, Information of physical position of sensors in needed, and how to convert from one to another. 

So here is the list of Sensors we are using data of.
1. 1 X [Velodyne HDL-64E Laserscanner](https://velodynelidar.com/blog/hdl-64e-lidar-sensor-retires/)
2. 4 X [FLIR Point Cameras](https://www.flir.eu/products/flea3-usb3/)
3. LiDAR and cameras use different systems to see and aren't in the same spot: it means that we're seeing an obstacle from 2 different positions with two different frames. We'll therefore need to convert the point seen by the LiDAR to the camera space, and then to the image space!

**Projection Formula:** Here is the formula to convert a point X in 3D into a point Y in 2D.

![Untitled Diagram drawio](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/efb273ae-f2ae-4842-8365-a02be995dab5)

above formula is highly dependent on our sensor setup system.

**P:**

A camera produces images by capturing light from the environment through its lens and converting it into a digital image. When buying a camera, it's typically pre-calibrated, meaning it's set up to produce images accurately without requiring you to adjust complex settings right away. This calibration ensures that the images you take are properly exposed and in focus.

Calibration is the process of teaching your camera how to translate a point in the real world (3D) into a pixel on the camera sensor. The intrinsic calibration matrix, the *P*, is a critical component in this process. It helps the camera understand the relationship between the 3D world and the 2D image it captures.

![Screenshot from 2023-09-15 17-29-21](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/84b24ca4-326a-4ded-8e9a-a1817fa74644)

In above matrix, f is is the focal length (fx, fy) and c is the optical center (cx, cy). This matrix is used to transform from the camera's perspective (camera frame) to the image's perspective (image frame).

**R0:**

In stereo vision, the aim is to make the left and right images line up perfectly, it helps in drawing a horizontal line across them, below are the same objects aligned with each other.

![image](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/48fcf638-4b26-4b9e-9d82-a7c6480ad607)

We refer to that horizontal line as the "Epipolar Line."

![image](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/5e70aa9d-d3f4-4b33-b1b2-dd24164cfb86)

In Stereo Vision, the matrix *R0* aligns the left and right images, making them match perfectly. This step isn't necessary with a single camera, but it's crucial for stereo vision to work correctly.

**R0|t:**

R|t is the transformation from the Velodyne frame of reference to the Camera frame of reference. It describes how data measured in the Velodyne's coordinate system can be translated and rotated to align with the coordinate system of the Camera.

![Untitled Diagram drawio(1)](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/e2b5e34c-1d3b-46f5-ab4f-c9e028c6fef9)
![l1 drawio](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/33b70df8-7c2e-4e8e-b565-d11a17934896)

In the above picture, Valedyne LiDAR Coordinate system is different from Camera Coordinate system. 

So we have to go from Velodyne coordinate system to Camera coordinate system, and this is called rotation. 

![2023_09_18_0pg_Kleki](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/09d8797a-1d8e-457f-8deb-a2d855e7b979)

And to move the coordinate system physically is called translation.

![2023_09_18_0pi_Kleki](https://github.com/SamiUddin-tech/LiDAR_Camera_Fusion/assets/81253183/e5151d4e-3a69-424b-84bc-08c894c17927)

**Keypoints:**
1. To project a point obtained from a LiDAR in an image, we need to understand clearly how are our sensors positioned, and what are their coordinate system.
2. The projection formula is Y = P * R0 * R|t * X
3. R|t is the matrix that convert a point from the Velodyne Frame to the Image frame. R0 is a matrix to rectify the stereo cameras. P is the intrinsic calibration matrix to take a point from the camera frame to the image (pixel).


**Applying the Projection Formula:**


**Projecting a 3D Point to 2D Image**

**

### 2. Obstacle Detection in 2D

This is what we do in object detection, given an image and output bounding boxes. And nothing more.



### 3. Fusing the Results

**Implementation of Object Detection and Sensor Fusion**


## Late Fusion

To do the late fusion, I performed 5 steps:

1. Detecting objects in 2D
2. Detecting objects in 3D
3. Projecting the 3D Bounding Box in the Image
4. Fusing the Bounding Boxes
5. Building the Ultimate 3D Object

### 1. Detect objects in 2D

### 2. Detect objects in 3D

### 3. Project the 3D Bounding Box in the Image

### 4. Fuse the Bounding Boxes

### 5. Build the Ultimate 3D Object

