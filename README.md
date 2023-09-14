# LiDAR_Camera_Fusion

In this Project I practiced some most advanced skills that Self Driving Car Engineers use to fuse LiDARs with Cameras.
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
In above Picture, which is adopted from [here](https://electrek.co/2016/10/20/tesla-new-autopilot-hardware-suite-camera-nvidia-tesla-vision/), it's the Tesla's Self Driving Vehicle Model. And notice that we have 3 cameras, one in left, one in right and one in the center, side cameras are generally called stereo pairs which makes it easy to estimate disance to an obstacle.

Another example of my OpenCV AI Kit with Depth [OAK-D](https://shop.luxonis.com/products/oak-d), Stereo Camera, which is architectured by [Brandon Gilles](https://www.linkedin.com/in/brandon-gilles-5400b734/) (Late) Founder of [LUXONIS](https://www.luxonis.com/) Robotic Perception Startup. Just Notice the Object Detection and Depth Perception (X,Y,Z), we get with [OAK-D](https://shop.luxonis.com/products/oak-d).
