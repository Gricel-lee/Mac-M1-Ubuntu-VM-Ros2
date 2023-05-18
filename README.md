# Welcome to ROS2 installation on MAC M1

## Requirements 
If you reached this github, you are trying to run ROS2 in Mac with a processor M1. Yeah, me too. 
After a lot of reading I decided to document this process just in case it works! :P

We will try to install ROS 2 Humble (Ubuntu Jammy) supported on Ubuntu 2.04.2 (https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debians.html#resources)

I decided to install it on a VM instead of a docker contained due to the lack of encoragment by the community and all the bad comments I read about actually working :P


## Install Ubuntu in a VM

Let's start by downloading UTM to create a virtual machine in Mac and Ubuntu 22.04.2 LTS (Jammy Jellyfish).
It is a bit tricky to find the Desktop ARM version for Ubuntu 22.04.2, hence here is the link:

https://cdimage.ubuntu.com/jammy/daily-live/current/

Make sure you download the ARM version, otherwise it won't run in the Mac M1 architecture.

Open UTM and create a virtual machine. Select the Ubuntu image downloaded from the link above (__jammy-desktop-arm64.iso__) and continue the process.

At the end you can start the virtual machine running Ubuntu. It would probably ask you for a user, enter ```ubuntu``` and leave the password blank. If all works well, we must wait a but until the Ubuntu desktop appears!

## Install ROS2

Now we can follow the instruction to install ROS2. Open a terminal and type the following (run it all together at your own risk!):

```
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8

locale  # verify settings

sudo apt install software-properties-common
sudo add-apt-repository universe

sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg

echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null

sudo apt update
sudo apt upgrade

sudo apt install ros-humble-desktop
sudo apt install ros-dev-tools
```
## Environment set up

Continuing with the ROS2 installation instructions, the next step is to set up the source file. For bash:

```
source /opt/ros/humble/setup.bash
```
(In my case, at this point I encounter the error of File not found when I reached this step. I needed to restart the process of installation from the beginning, it may be I didn't save the VM as I turned it off... oh well)

Finally we can run the example in two terminals:

Terminal one (publisher):

```
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_cpp talker
```

and terminal 2 (listener):

```
source /opt/ros/humble/setup.bash
ros2 run demo_nodes_py listener
```
