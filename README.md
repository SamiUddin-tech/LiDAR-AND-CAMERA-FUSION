# LiDAR_Camera_Fusion

In this Project, I practiced some most advanced skills that Self Driving Car Engineers use to fuse LiDARs with Cameras.
LiDAR is used more and more in almost every robotics startup, and mixing it with a camera is really cool!

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

## Early Fusion

To perform early fusion I performed three steps:

1. Project the Point Clouds (3D) to the Image(2D)
2. Detect Obstacles in 2D (Camera)
3. Fuse the Results

