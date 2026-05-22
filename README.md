# How to Install Ubuntu on Windows Using WSL2

## Intro

In this tutorial, I’ll show you how to install Ubuntu on Windows using WSL2. This lets you run Ubuntu Linux directly inside Windows without deleting Windows or dual booting.

We’ll set everything up step by step so you can prepare for future ROS 2 tutorials.

---

# Step 1 — Check Windows Version

Press:

```text
Windows + R
```

Type:

```text
winver
```

Press ENTER.

You should ideally have:

- Windows 10 version 2004+
- or Windows 11

---

# Step 2 — Open PowerShell as Administrator

1. Press the Windows key
2. Search for:

```text
PowerShell
```

3. Right-click it
4. Select:

```text
Run as Administrator
```

---

# Step 3 — Install WSL2 and Ubuntu 24.04

Run this command:

```bash
wsl --install -d Ubuntu-24.04
```

This is the most important step.

We are specifically asking for Ubuntu 24.04 because future robotics software (like ROS 2 Jazzy) requires this exact version to work.

This command installs:

- WSL2
- Ubuntu
- The required virtualization components

---

# Step 4 — Restart Computer

After the installation finishes:

Restart your PC.

This is required.

---

# Step 5 — Open Ubuntu

After reboot:

1. Press the Windows key
2. Search:

```text
Ubuntu
```

3. Open it

Ubuntu will finish installing automatically.

---

# Step 6 — Create Linux Username & Password

Ubuntu will ask:

```text
Enter new UNIX username:
```

Example:

```text
{your_name}
```

Then:

```text
Enter new UNIX password:
```

The password will NOT appear while typing.

This is a normal Linux security feature.

Just type it and press ENTER.

---

# Step 7 — Verify Ubuntu Version

Inside the Ubuntu terminal, run:

```bash
lsb_release -a
```

Look at the `Description` line.

It should say:

```text
Ubuntu 24.04 LTS
```

This confirms we are ready for ROS 2.

---

# Step 8 — Update Ubuntu

Run this command:

```bash
sudo apt update && sudo apt upgrade -y
```

Explanation:

- `sudo` = Administrator privileges
- `apt update` = Refreshes package lists
- `apt upgrade` = Installs the latest updates

---

# Step 9 — Verify Ubuntu Works

Run:

```bash
ls
```

Then run:

```bash
pwd
```

Explanation:

- `ls` lists your files
- `pwd` shows your current directory

Welcome to Linux basics.

---

# Step 10 — Install VS Code

Download and install Visual Studio Code on Windows normally.

---

# Step 11 — Install WSL Extension in VS Code

Inside VS Code:

1. Open the Extensions tab
2. Search:

```text
WSL
```

3. Install the extension named:

```text
WSL
```

Made by Microsoft.

---

# Step 12 — Open Ubuntu Inside VS Code

Back inside your Ubuntu terminal, run:

```bash
code .
```

This opens VS Code connected directly to your Ubuntu environment.

> Note: If the `code` command fails, open VS Code manually once, close it, and retry.

---

# Step 13 — Verify Everything Works

Inside the VS Code terminal, run:

```bash
uname -a
```

You should see Linux kernel information.

This confirms Ubuntu is running correctly inside VS Code.

---



# How to Install ROS 2 Jazzy on Ubuntu (WSL2)

# Step 1 — Open Ubuntu (WSL2)

1. Press the Windows key
2. Search:

```text
Ubuntu
```

3. Open it

Or simply type:

```text
wsl
```

inside Windows Terminal.

---

# Step 2 — Update System Packages

Inside the Ubuntu terminal, run:

```bash
sudo apt update && sudo apt upgrade -y
```

Updating packages first helps prevent installation issues later.

---

# Step 3 — Set Locale (Important for ROS 2)

Run these commands one by one:

```bash
sudo apt update
sudo apt install locales -y
sudo locale-gen en_US en_US.UTF-8
sudo update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
export LANG=en_US.UTF-8
```

ROS 2 requires specific language and character encoding settings to function properly.

---

# Step 4 — Enable Universe Repository

Run:

```bash
sudo apt install software-properties-common -y
sudo add-apt-repository universe
```

---

# Step 5 — Add ROS 2 GPG Key

Run:

```bash
sudo apt update && sudo apt install curl -y
sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
```

---

# Step 6 — Add ROS 2 Repository

Run this command as one single line:

```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu noble main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
```

---

# Step 7 — Install ROS 2 Jazzy Desktop

Run:

```bash
sudo apt update
sudo apt install ros-jazzy-desktop -y
```

This installs:

- Core ROS 2 libraries
- Visual tools like RViz

This step may take several minutes.

---

# Step 8 — Source ROS 2 Environment

Run:

```bash
echo "source /opt/ros/jazzy/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

This automatically activates ROS 2 every time you open a terminal.

---

# Step 9 — Install ROS 2 Developer Tools

Run:

```bash
sudo apt install python3-colcon-common-extensions python3-rosdep -y
```

---

# Step 10 — Initialize rosdep

Run:

```bash
sudo rosdep init
rosdep update
```

---

# Step 11 — Test ROS 2 Installation

Run:

```bash
ros2 topic list
```

Expected output:

```text
/parameter_events
/rosout
```

If you see these lines, ROS 2 is working correctly.

---

# Step 12 — Create Your First Workspace

Run:

```bash
mkdir -p ~/ros2_ws/src
cd ~/ros2_ws
colcon build
```

---

# Step 13 — Open VS Code (WSL)

Run:

```bash
code .
```

This opens your ROS 2 workspace directly inside VS Code, ready for development.

# FlowCore (YouTube): https://www.youtube.com/@fcai_comp
Happy coding! :)

