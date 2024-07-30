# tutorial_test
## Table of contents

1. About this repository
2. Intro and general consepts
    - ROS 2 (Humble)
    - WEBservers/websocket
3. Enviroment, OS and preperation
    - Install UBUNTU on VirtualBox on Windows
    - Installing UBUNTU on VirtualBox or UTM on MAC OS
    - Using different hardware (Laptop/PC, Rasberry Pi, latepanda)
    - Installing ROS (2 Humble) on UBUNTU 
    - Installing a code editor on UBUNTU
    - Creating a simple WebSocket in UBUNTU
3. Usecase: control arduino LED via WEB socket using ROS2 (Humble)
4. Usecase: control RPi Pico via web socket using microros 
5. Usecase: control arduino LED via websocket (? if time allows)
7. Useful resources
    - links to resources
    - useful libraries, commands and packages


# About this repository
# Intro and general consepts
  The projects in the **NAME HERE** repository are individual, yet they share some similarities. The unique physical setup with a tablet handling the **add tablet name** collecting user input via a web application, an independent robot (arduino, Pi etc) executing the commands requiers a mediator. A computer which recieves user imput from the tablet and informs the robot what to do. In this tutorial we will use ROS2  and websocket to achieve this.
## Webservers/websocket
  A webserver is responsible to serve content like like web pages, to users "clients" over the internet. Browsers send requests to a webserver adn the server finds the requested content and replies to the client. Typically, a webserver processes individual requests from a browser, sending back responses each time, and then the connection closes. This works well for static content, for example a website, but is less efficient for interactive applications where information changes frequently. Like for example controlling a robot.
  
  For these types of applications we use a WebSocket. A WebSocket allows a server to maintain a continuous, real-time, two-way communication with it's client. Communication can be lean and fast which is very beneficial in our case.

  The way that the **add tablet name** works is by using the **name here** as a mouse and allowing the user to focus their eyes in different areas on the screen to make a choice. The browser percives this action as a simple mouse "hoover" over a block or button. since the **add name** is not very persise it is adviced to make these buttons oversized and keep the options limited. For example "left" "right" "shoot" could be establiched in this way.

  ![buttons](images/buttons.png)

# Enviroment, OS and preperation

ROS2 (much like many opesource open-source frameworks) is simplest to install and use in Linux operating systems. 
It is possible to install and use ROS2 on WIndows and Mac OS enviroments. In fact there are tutorials from the official ROS documentation such as [ROS2 for MAC](https://docs.ros.org/en/crystal/Installation/macOS-Install-Binary.html) and [ROS2 for Windows](https://docs.ros.org/en/crystal/Installation/Windows-Install-Binary.html) that you can follow. Additionally if you already have ROS2 installed in your working enviroment there is no reason to add any extra virtual enviroments and you can skip this step entierly. Though for begginer users we are recomending to have a UBUNTU instalation or a Virtual Machine (VM) as it will be cleaner and easier to manage in the logn-run. For this tutorial we will be using UBUNTU 22. 

Next you will find two short tutorials for installing Virtualbox and setting up your UBUNTU 22 enviroment on Windows and MAC OS.


## Install UBUNTU on VirtualBox on Windows

1.  Download Oracle VM VirtualBox
	
	- You can download the .exe file from the official site and install it like any other program.

2.  Download the Linux 22.04 version (jammy jelly) ISO file (image).

	- This version, albeit older, is fully supported by the ROS2 Humble. So in order to download the iso, click the following link: [Ubuntu 22](https://releases.ubuntu.com/jammy/ubuntu-22.04.4-desktop-amd64.iso)
	

3. Having both the ISO image and the VirtualBox, we are ready to create a new virtual machine. To do this, click on **Machine** on the Top Menu and then click on **New**. Then fill in the details:

	- **Name**: The name of the Virtual Machine (Typically we use the operating system's name).
	- **Machine Folder**: The place in your computer where all virtual machines will be stored.(You can leave the default one if you like).
	- **ISO image file**: From the drop down menu, choose the iso image file you downloaded earlier.

	![create VM](images/1create_vm.png)

4. After clicking **Next**, you will be prompted to create a User Profile. On this step, changing the default credentials is crucial since if not, the user created will not have sudo access over the system. So, choose a user name and password to your liking and click **Next**.


	![](images/2user_profile.png)

5. In the next window, you will have to define the resources the virtual operating system will use. Here it is recommended to allocate at least 8GB of Base Memory and 4 CPUs. After choosing the preferred settings, click on **Next**. 

	![](images/3resources.png)

6. Next, you will have to define the Hard Disk Size in which the operating system will be installed. Generally, it is recommended to allocate at least 25GB of Disk Size, but if you are planning on using the Virtual Machine for large projects, adjust the size accordingly.

	![](images/4disk_size.png)

7. After clicking **Next**, a window with a summary of your virtual machine will pop up. There you can review all the settings you configured in the previous steps. If everything is ok, click on **Finish** and the installation process will begin.

8. During the installation, you will be prompted to pick a user name and a password in order to log in. Fill in the blanks ad press **Continue**. Make sure you save this login details as they will be asked in the next step

	![](images/5user_pass.png)

9. Afterwards the installation will proceed and in the end, you will have to log in with the credentials from the previous step. Insert your password and the ubuntu image will run.

	![](images/6login.png)

### Installing Guest Additions

- Guest Additions extends the utilities of the guest system. For example, it enables it to connect with external devices or have shared folders with the host system. 
**In order to be installed properly, it is important to follow these steps:**

1. Power up the Virtual Machine.
2. Make sure that our Ubuntu system gcc module version is 12. We can achieve this by doing the following:
	- Open the terminal and run: 
			
    `sudo apt install --reinstall gcc-12`
		
  - Then update the link for gcc to go to the gcc-12 binary by running: 
			
    `sudo ln -s -f /usr/bin/gcc-11 /usr/bin/gcc`


3. Now, on the Top Menu of the Operating System running window, click on **Devices** and then click on **Insert Guest Additions CD Image**.
	
	![](images/Devices.png)


4. A CD Icon should appear. Click on it for the folder to open.
		
	![](images/cd_icon.png)

5. Then, right click anywhere in the folder and click **Open in Terminal**.This should open a terminal with a command prompt for this directory and run: 

`./autorun.sh`

And with that, we installed Guest Additions.

### Installing UBUNTU on VirtualBox or UTM on MAC OS


1.  Download your choice of virtualization tool

For MAC OS we can suggest 2 virtualization tools:

  - If you are having an intel-based Mac downloading Virtualbox is pretty straight forward you can download the .dmg file from the [official site](https://www.virtualbox.org/wiki/Downloads) \(choose the ​macOS / Intel hosts one\). and you can follow the rest of the steps as described above. Or you can use UTM as instructed bellow which is MAC specific and therefore tends to be more optimised for MACs. 

  - At the time of writting this instructions the **M1 and M2 chips** are not fully supported for the latest version of Virtualbox and UBUNTU. A native MAC virtual machine emulator and virtualiser is [UTM](https://mac.getutm.app) for M1/M2 chips UTM is suggested. You can find documentation to customise your virtual enviroment [here](https://docs.getutm.app). 

  - Download the .dmg from [the UTM website](https://mac.getutm.app) and install it like any other program.
  ![UTM install](images/mac/1mac_instal.png)

2.  Download the Linux 22.04 version (jammy jelly) ISO file (image).

	- For Mac OS you will have to download **jammy-desktop-arm64.iso** [from this link](https://cdimage.ubuntu.com/jammy/daily-live/current/).
	

3. Having both the ISO image and UTM, we are ready to create a new virtual machine. To do this follow the next steps:

  - Click on the **Create New Machine** option, then click on **Virtualise** and select **Linux**. 
    ![create VM](images/mac/2new_machine.png)
    ![create VM](images/mac/2_1new_machine.png)
    ![create VM](images/mac/2_2new_machine.png)
  - On the next window select **Boot from Kernel Image** 
    ![create VM](images/mac/2_3new_machine.png)
  - Scroll down and click on the browse button of the **Boot ISO Image (optional)** option. Then navigate to the ubuntu iso image you downloaded, select it and click **Open**.
    ![create VM](images/mac/2_4new_machine.png)
    ![create VM](images/mac/2_5new_machine.png)
  

4. After clicking **Continue**, you will be prompted to define the resources the virtual operating system will use. Here it is recommended to allocate at least **8GB of Base Memory and 4 CPUs**. After choosing the preferred settings, click Continue.

  ![user](images/mac/3resources.png)

5. Next, you will have to define the Hard Disk Size in which the operating system will be installed. The default value is 65G but generally, it is recommended to allocate at least 25GB of Disk Size, but if you are planning on using the Virtual Machine for large projects, adjust the size accordingly.

  ![user](images/mac/4disk_space.png)

6. Next, you will have to define the Hard Disk Size in which the operating system will be installed. Generally, it is recommended to allocate at least 25GB of Disk Size, but if you are planning on using the Virtual Machine for large projects, adjust the size accordingly.

	![disk size](images/mac/4disk_size.png)

7. Next you will have to locate the shared folder between yout host machine (your MAC OS) and the guest machine (the UBUNTU). Create a new folder anywhere in your file system.  Remember that the virtual machine will have access **ONLY** on this folder.

  ![disk size](images/mac/5shared_dir.png)

8. After clicking **Continue**, a window with a summary of your virtual machine will pop up. There you can review all the settings you configured in the previous steps. Here you can set a name of the Virtual Machine (Typically we use the operating system's name). If everything is ok, click on **Finish** and the installation process will begin.

  ![disk size](images/mac/6summary.png)

9. After the set-up is complete you can boot your machine from UTM. This will boot Ubuntu 22.04 from the ISO image. Follow the installation steps and select reboot.

  ![boot](images/mac/7boot.png)
  ![boot](images/mac/7_1boot.png)
  Choose **Try or Install UBUNTU**.
  - You will be landing on your UBUNTU desktop where you need to click on the iso image and follow the instructions to install your UBUNTU OS. 
  ![desktop](images/mac/8desktop.png)
  - During the installation, you will be prompted to pick a user name and a password in order to log in. Fill in the blanks ad press **Continue**. Make sure you save this login details as they will be asked when you log in to UBUNTU.
  ![warnings](images/mac/8user.png)
  - Do not worry over this message. The VM only has access on the allocated Disk space and it will never affect your host OS.  
  ![warnings](images/mac/9warnings.png)
  - At the end of the installation select **Continue testing** and instead of rebooting **Power Off** the machine.
  ![reboot](images/mac/10reboot.png)

10. Boot your UBUNTU machine. This virtual machine is currently considerring the .iso image as a CD/DVD drive and will boot from it again. In order to avoid that you will need to **Clear the CD/DVD** From UTM. You can find it at the bottom of the VM's satus page.
![remove image](images/mac/11clear_image.png)
After that you can boot your UBUNTU normaly.

11. Share files and Clipboard with your virtual UBUNTU on UTM

- You can find documentation to customise your virtual enviroment [here](https://docs.getutm.app). For this installation we advise to install packages that will allow you to share some files with your host OS (your MAC) as well as your clicpboard so you can copy paste from one to the other. 

  - Open the terminal and run:

    `sudo apt install --reinstall gcc-12`
 
  - Then update the link for gcc to go to the gcc-12 binary by running:
    
    `sudo ln -s -f /usr/bin/gcc-12 /usr/bin/gcc`
  
  - Navigate to the 'Software updater' tab and make sure these 4 option are selected. 
  ![create VM](images/mac/1_1sharing.png)
  ![create VM](images/mac/1_2sharing.png)
  - Then install the spice-webdavd package and reload the VM.
    
    `sudo apt install spice-vdagent spice-webdavd`
## Using different hardware
So far we have covered using a laptop or PC running Linux, Windows or MAC OS. While this is the most common hardware we might want/need to control our robot from a rasberry Pi or latepanda depending on our project. 

In the case of Rasberry Pi we suggest selecting a 64-bit Pi in order to ensure that you can have the easiest time installing and running ROS2 as you can see in the [official documentation](https://docs.ros.org/en/humble/How-To-Guides/Installing-on-Raspberry-Pi.html). Rasberry OS (formerly known as rasbian) is Debian based and therefore the above settings for UBUNTU should work on it with minor diversions. Extra applications such as an IDE like Visual Studio Code can be chosen depending on the Pi's specifications (disk, ram etc). Visual Studio Code [is available for Rasberry OS](https://code.visualstudio.com/docs/setup/raspberry-pi). 

Similarly, if we want to use latepanda in our project we can install UBUNTU 22.04 directly onto it [using this official documentation](https://docs.lattepanda.com/content/3rd_delta_edition/Operating_Systems_Ubuntu/). 


##  Installing ROS (2 Humble) on UBUNTU 

After setting up a Linux (in this case UBUNTU) operating system in our machine we are ready to install and set-up ROS 2 Humble. Which should be the same process regardless from which OS we started from. We will setup UTF-8 encoding, download and install ROS 2.

### Locale setup to UTF-8

First, we make sure that we have a system locale that supports UTF-8. We can check if UTF-8 is supported by running the command: `locale`. If the result is something like the following, we are good to go:

LANG=en_CA.UTF-8
LANGUAGE=en_CA:en
LC_CTYPE="en_CA.UTF-8"
LC_NUMERIC=en_AU.UTF-8
LC_TIME=en_AU.UTF-8
LC_COLLATE="en_CA.UTF-8"
LC_MONETARY=en_AU.UTF-8
LC_MESSAGES="en_CA.UTF-8"
LC_PAPER=en_AU.UTF-8
LC_NAME=en_AU.UTF-8
LC_ADDRESS=en_AU.UTF-8
LC_TELEPHONE=en_AU.UTF-8
LC_MEASUREMENT=en_AU.UTF-8
LC_IDENTIFICATION=en_AU.UTF-8
LC_ALL=

If not, however, we run the following commands:

```
sudo apt update && sudo apt install locales
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

### ROS 2 repository

In order to keep ROS 2 up-to-date, we need to add the ROS 2 apt repository to the system. To achieve this we follow these steps:

- Make sure the the Ubuntu Universe Repository is enabled:

```
sudo apt install software-properties-common
sudo add-apt-repository universe
```

If it is not, after running the second command, it will ask to press enter to enable.

- Add the curl utility and the ROS 2 GPG key:

```
sudo apt update && sudo apt install curl -y

sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

- Add the repository to the sources list:

```
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(. /etc/os-release && echo $UBUNTU_CODENAME) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

### Install ROS 2

Now that the repositories are set up, ROS 2 can be installed.

- Update the apt repository cache: 
`sudo apt update`
- Upgrade the system: 
`sudo apt upgrade`

Install ROS 2 by running the following command:

```
sudo apt install ros-humble-desktop
```


### Check installation

- If all went well, ROS 2 should be ready to be used. We can check this by sourcing the terminal with the command:

  ```
  source /opt/ros/humble/setup.bash
  ```

- Sourcing ROS 2 is something that we need to do in every terminal we open, it allowes the terminal to "know about" ROS 2. In order to avoid running this command every time we can add it to our setup.bash file:

  ```
  echo "source /opt/ros/humble/setup.bash" >> ~/.bashrc
  ```


and then run:

  ```
  ros2 --help
  ```


If the result is the following, everything worked correctly.

![ros_help](images/ros_help.png)

It is important to note that the source comand reads and executes commands from a file in the **current** shell environment. The /opt/ros/humble/setup.bash script is a setup file installed by ROS 2 that configures the environment variables and paths necessary for using ROS 2. We will need to run the same command on every terminal window we want to use ROS 2 in, even if we open a new tab in the termal window we are working in. We can always check if a terminal shell is aware of ROS 2 via the `ros2 --help` command.
![2terminal](images/mac/double_terminal.png)

## Installing a code editor on UBUNTU
  In order to start programming we will need a code editor. Freel free to install your favourite editor, or use the one you already have. For the purposes of this tutorial we will use Visual Studio Code.

### Installing Visual Studio Code on UBUNTU 

#### Using the snapstore GUI

- First we need to  download the installation file. We naviage to the VS Code page:

  ![vsweb](images/vs_web.png)
and we click on the .deb button. A .deb file will be downloaded as a result.

- Then, double click on the .deb file and a window will pop up 

  ![](images/deb_file.png)
  (If this is not the window that popped up, close it, then right-click on the .deb and click on **Open with another application**).

- Click the select button and the snap store will appear.
  ![](images/snap.png)

- Click on **Install** and after the process is finished, the VS Code application is installed and ready for use.

#### Using the terminal (ARM64 specific)

In most cases the above process should work, though if you are having a UBUNTU running on a MAC OS host you will most likely have an ARM64 architecture in which VScode is not readily available. In this case the IDE will have to be installed using the comand line.

- Depending on your systems architecture you will need to install the correct package. 
- For ARM64:
  - Open a terminal and use wget to download the latest ARM64 .deb package of Visual Studio Code:
  ```
  wget https://update.code.visualstudio.com/latest/linux-deb-arm64/stable -O code_arm64.deb
  ```
  - Install the package
  ```
  sudo apt update
  sudo apt install ./code_arm64.deb
  ```
- For amd64:
   - Open a terminal and use wget to download the latest ARM64 .deb package of Visual Studio Code:
  ```
  wget https://update.code.visualstudio.com/latest/linux-deb-x64/stable -O code_amd64.deb
  ```
  - Install the package
  ```
  sudo apt update
  sudo apt install ./code_amd64.deb
  ```

- In order to open Visual Studio Code you can now either type `code` on the terminal or search "Visual Studio Code" on the Show applications tab.
![visual_studio](images/mac/visual_studio.png)

## Setting up VScode for ROS2 projects
Before starting to use the ROS 2 framework for our projects, we need to setup our environment.

### Setting up VS Code

Now that VS Code is installed open it from **Show Applications**, on the bottom left corner. It should be looking like this:

![vs_open](images/vs_open.png)

Now, on the left bar menu, click on the **Extensions** tab and search for the following extensions:

- Python:

![python](images/python.png)

- C/C++:

![c](images/c.png)

- ROS:

![ros](images/ros.png)

- CMake and CMake Tools:

![cmake_tools](images/cmake_tools.png)


## Terminator

- Though not mandatory, Terminator is a very useful terminal and really popular for creating robotics projects. It is recommended since it will make our lives easier, since it is able to create terminals by splitting the window and thus, multiple terminals can be accessed simultaneously. To install, run the command:

  ```
  sudo apt install terminator
  ```

- Then, open Terminator and try to split terminals by pressing **ctrl + shift + E** and **ctrl + shift + O**. The result will be this:
![terminator](images/terminator.png)

## Colcon

Colcon is the build command for ROS 2. We need to set it up seperately by running the following command:

```
sudo apt install python3-colcon-common-extensions
```

## Installing ROS 2 packages

In general, ROS 2 offers a lot of packages(libraries) for different applications. Some notable once are Gazebo and Controller. For the purposes of this tutorial we will need two packages:

- Rosbridge
- Micro-ROS

These packages will be crucial to our project. For the first we just need to run the following command:

```
sudo apt install ros-humble-rosbridge-suite
```

For the second we need to clone the git repository so we can download the library:

```
sudo apt install git
```

Then, install rosdep to check for ros dependencies during the installation (It als needs to be initialized only once after the installation).

```
sudo apt install python3-rosdep
sudo rosdep init 
```

If, for some reason, python is not installed in your system, you can install it by following this guide:https://www.geeksforgeeks.org/how-to-install-python-on-linux/

Lastly, we need to install pip (package manager for python).

```
sudo apt install python3-pip
```

Now that we have installed the prerequisites, we can install micro-ROS library for ROS-Humble.

- Then, we will create a new workspace in which we will clone the git repository so we can use the micro-ROS tools. For this tutorial we have created "Projects/ROS2-tutorial" where we will place the workspace folder

```

cd Projects/ROS2-tutorial
mkdir microros_ws
cd microros_ws
git clone -b humble https://github.com/micro-ROS/micro_ros_setup.git src/micro_ros_setup
```

The previous code creates a workspace where micro-ROS tools can be used. 

- We update dependencies by using the rosdep command:

```

sudo apt update && rosdep update
rosdep install --from-paths src --ignore-src -y
```

- Lastly, we will build the micro-ROS tools and source them:

```
colcon build
source install/local_setup.bash
```

With this we have a completely set up environment so we can start our projects.


## Creating a simple WebSocket in UBUNTU

For this tutorial we will be using Node.js for building the Websocket application. We have selected Node.js ammongst the many available options (for example Python websockets, Java Spring Boot, Gorilla WebSocket etc) due to the several benefits it provides (event-driven, non-blocking architecture, real-time connections, extensive libraries etc) though if you feel you are more comfortable with other languages and libraries feel free to use them, it will not affect project overall.

### Handle Prerequisites

- Install Node.js and npm

```
sudo apt update
sudo apt install nodejs npm
```

- Create a folder for the project For this tutorial we have created "Projects/ROS2-tutorial/server" where we will create the websocket. 
  **NOTE:** In Ubuntu you can right-click on a folder and open it directly on a new terminal tab.
  ![2terminal](images/server_folder.png)
- Create the file package.json with the following code:

_______________________
websocker code here
_______________________
