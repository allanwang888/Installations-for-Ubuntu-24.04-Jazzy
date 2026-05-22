# How to Install Ubuntu 24.04 (WSL2) & ROS 2 Jazzy on Windows

A complete, step-by-step tutorial on how to set up Ubuntu 24.04 and ROS 2 Jazzy for high-performance robotics development directly inside Windows.

> **MAC USERS:** This tutorial uses WSL2, which is exclusive to Windows. These commands will not work on macOS. You will need to use a Virtual Machine (such as UTM or Parallels) to install Ubuntu 24.04.

---

# Part 1: Setting up Ubuntu 24.04 via WSL2

## 1. Check Your Windows Version

Press `Windows + R`, type:

```text
winver
```

Then hit **Enter**.

Make sure you are using:

- Windows 10 version 2004 or newer
- OR Windows 11

---

## 2. Open PowerShell as Administrator

1. Press the Windows Key
2. Search for **PowerShell**
3. Right-click it
4. Select **Run as Administrator**

---

## 3. Install WSL2 and Ubuntu 24.04

Run the following command:

```bash
wsl --install -d Ubuntu-24.04
```

Restart your computer once the installation finishes.

---

## 4. Initialize Ubuntu

After rebooting:

1. Search for **Ubuntu** in the Windows Start Menu
2. Open it
3. Create your UNIX username and password when prompted

> Your password will not appear while typing. This is normal Linux behavior.

---

## 5. Verify Your Ubuntu Version

Ensure you are running Ubuntu 24.04 (Noble Numbat):

```bash
lsb_release -a
```

---

## 6. Update Ubuntu

Keep your Linux subsystem updated:

```bash
sudo apt update && sudo apt upgrade -y
```

---

# 🛠️ Part 2: Installing ROS 2 Jazzy

## 1. Set the Locale

ROS 2 requires specific locale settings.

Run these commands one by one:

```bash
sudo apt update
sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

---

## 2. Enable the Universe Repository

```bash
sudo apt install software-properties-common -y
sudo add-apt-repository universe
```

---

## 3. Add the ROS 2 GPG Key

```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

---

## 4. Add the ROS 2 Repository

Copy and paste this entire command as one single line:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu noble main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

## 5. Install ROS 2 Jazzy Desktop

This installs the ROS 2 core libraries and GUI tools like RViz.

```bash
sudo apt update
sudo apt install ros-jazzy-desktop -y
```

> This installation may take several minutes.

---

## 6. Source the ROS 2 Environment

Automatically activate ROS 2 whenever a new terminal opens:

```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

---

## 7. Install Developer Tools & Initialize rosdep

```bash
sudo apt install python3-colcon-common-extensions python3-rosdep -y
sudo rosdep init
rosdep update
```

---

## 8. Test Your Installation

Check whether ROS 2 is functioning correctly:

```bash
ros2 topic list
```

You should see:

```text
/parameter_events
/rosout
```

If you see these topics, ROS 2 is installed successfully

---

# (Part 3: Creating Your First Workspace)

Now let's create a ROS 2 workspace for your future robotics projects.

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
```

---

# (Open Your Workspace in VS Code)

If you have:

- Visual Studio Code installed on Windows
- The official **WSL Extension** installed

You can open your ROS 2 workspace directly from Ubuntu:

```bash
code .
```

---

# (Congratulations!)

You now have:

- Ubuntu 24.04 running inside Windows using WSL2
- ROS 2 Jazzy fully installed
- A working ROS 2 workspace ready for robotics development



# FlowCore (YouTube): https://www.youtube.com/@fcai_comp
Happy building!
