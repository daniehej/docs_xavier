# Getting Started
The AGX Xavier does not have an operating system installed by default

In order to flash an operating system on the Jetson AGX Xavier, it is necesary to use a computer running Ubuntu 18.04 (Update: As of 2022, it should also be possible to use Ubuntu 20.04). The SDK manager does not support other operating systems or newer versions of Ubuntu.

If you do not have a computer running Ubuntu 18.04, you can use a virtual machine in VMware to run the SDK Manager. See [Virtual Machine Setup](#virtual-machine-setup).

On the side of the unit, there are three buttons which are laid out as follows.

![Button Layout](https://git.its.aau.dk/WW82ZE/docs_xavier/raw/branch/master/img/xavier.png)


## Setup

1.  Unpack the Nvidia Jetson AGX Xavier

2.  Use the USB-C cable to connect the front USB-C port to a PC running Ubuntu 18.04. The front is the side with the GPIO pins and micro USB debugging interface

3.  Go to <https://developer.nvidia.com/nvidia-sdk-manager> and download the SDK manager

4.  On the Jetson press and hold the "Force Recovery" middle button and then press the
    power button on the left, then release both

5.  Run SDK Manager

6.  Select manual setup and accept the license

7.  Wait for the installation and the flashing of the Jetson to complete

8.  Plug in keyboard, mouse and screen. You can plug in two USB devices using the USB-A/eSATA combiport and the USB-C to USB-A cable 

9.  Run the basic setup on the Jetson, and choose a username/password, e.g. nvidia/nvidia

10. Input the IP `192.168.55.1` and username/password to the SDK Manager to install the SDK


## First Use
- After installing the SDK, you can change the power setting in the top menu bar. The default is "MODE_10W". Set the power setting to "MAXN" for max performance and max power usage.

- To update the system run the commands `sudo apt update` and `sudo apt upgrade`


## Virtual Machine Setup
On the support forums, Nvidia states that a physical computer running Ubuntu 18.04 is required. However, it is in fact possible to flash the Jetson from a Virtual Machine as long as VMware is used as the virtualization solution. Virtualbox does not give good results since its USB passthrough is not good enough.

AAU has a license for VMWare. It can be downloaded from <https://www.ekstranet.its.aau.dk/software/vmware>. Alternatively you can use the free VMWare Player.

1.  Go to <https://releases.ubuntu.com/18.04/> to download Ubuntu 18.04

2.  Open VMware and create a new VM

3.  Set up the VM with the following hardware configuration:

    1.  At least 3 GB RAM

    2.  At least 2 cores

    3.  At least 80 GB storage space

    4.  Configure the VM to use USB 3. This is important
        for speeding up the flashing process

4.  Install Ubuntu in the VM

5.  (Optional) Once Ubuntu is installed, if you want to drag and drop files into the VM, you need to install
    open-vm-tools for resolution scaling and clip board sharing:

    1.  `sudo apt update && sudo apt -y upgrade && sudo apt -y install open-vm-tools open-vm-tools-desktop`

    2.  Reboot when done

6.  Connect the front USB-C on the Jetson to your host computer

7.  In the VMware window find the USB section in the top menu bar

8.  Find the Nvidia Jetson device and select it

At this point the Jetson Xavier should be connected to the Ubuntu VM