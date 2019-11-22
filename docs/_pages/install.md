---
permalink: /install/

title: "Installation and use"

sidebar:
  nav: "docs"
---

The current setup I'm developing on is a Nvidia Jetson TX1, which is a powerful embedded device to perform such heavy tasks as deep learning inferences on real time. It is mounted on top of a Turtlebot2 robot, capable of supply a DC source to keep it on.

Combining these two devices, we have a fully autonomous robot, which can be remotely programmed or controlled without physical presence. This is such a great leverage when developing this project, as it will accelerate the workflow.

The main drawback of the Jetson device is the low resources we count on: just a 16GB eMMC storage device, and 4 GB of shared memory for both the CPU and GPU. Hence, we have to squeeze out every drop of performance we can achieve, so it's fundamental to keep the infrastructure as tight as possible. The first taken measure is to attach a SATA storage (our choice was a 120 GB SSD) to work as our main workspace. The second step is to install the latest possible version of each software component.

# Requirements

* __Nvidia JetPack 4.2.2__: installed using the [official Nvidia SDKManager tool.](https://developer.nvidia.com/nvidia-sdk-manager). This build incorporates CUDA 10.0 and the TensorRT engine on its version 5.

* __Python 3.6__: as Python 2.7 is close to its official end-of-life date, we have migrated to Python 3 development. It can be installed with the standard APT repository:
```bash
sudo apt install python3 python3-dev python3-pip
```
* __ROS Melodic__: the latest ROS LTS version, which in addition is the only one supported by Ubuntu 18.04 (the Ubuntu version packed on JetPack 4.x). It can be installed following the [simple installation instructions provided in the official website.](http://wiki.ros.org/melodic/Installation/Ubuntu) A couple of required packages have to be installed manually. The process is flawlessly explained [in this Medium blog.](https://medium.com/@beta_b0t/how-to-setup-ros-with-python-3-44a69ca36674)

* __OpenCV 4__: mandatory library on Computer Vision tasks. An important thing to notice is that the widely used 2.x and 3.x versions, which can be easily found on the Internet and repositories to install present a bug on the ARM compilation, which is just the version we have to use due to the Jetson CPU architecture. This results on an __extremely slow image rendering time__ (a simple `cv2.imshow()` call can take a huge time when compared to the rest of the program execution time). However, this problem has been tackled and solved on the 4.x version, which is the one we have to install. [This wonderful blog on pyimagesearch explains the process of compilation without major trouble.](https://www.pyimagesearch.com/2018/08/15/how-to-install-opencv-4-on-ubuntu/) Notice that, if you decide to create a virtual environment (which I strongly encourage you to do), you will have to activate for the rest of the installation tasks, as well as every time you want to execute the program.

* __TensorFlow 1.14.0__: the last TF1.0 version before the jump to TF2.0. Another advantage of having installed the latest JetPack version and using Python 3 is that we can just [download the already compiled TF package by Nvidia themselves](https://developer.nvidia.com/embedded/downloads#?search=tensorflow), which offers total compatibility with the GPU engine of our Jetson TX1. Our labour here gets reduced to download the `.whl` file and issue this command __inside the created virtualenv__ (otherwise it might not be correctly imported when executing the program):
```bash
pip install {thefile}.whl
```
Isn't that great?

At last, we just have to install a couple of ROS packages to enable the usage of our specific hardware (the kobuki robot and Xtion RGBD camera):
```bash
sudo apt install ros-melodic-openni2-launch ros-melodic-kobuki-node
```

# Install

On this moment, the software on the repository is functional, although we are still working on the migration from the Python 2 framework, as well as polishing the inference processes.

# Usage

Open a Python console and

```python
import time
while True:
    time.sleep(1)
```
Check back this page in a while to try a functional version of the software!