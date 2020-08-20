# Pycharm Remote Interpreter
It is possible to run a remote Python interpreter on the Jetson AGX Xavier. This lets you write your scripts in Pycharm on your own computer and execute them on the Xavier to utilize its computing power.

Remote interpreters are only supported in Pycharm Professional. A license is free for educational use: [https://www.jetbrains.com/community/education/](https://www.jetbrains.com/community/education/).


## Prerequisites
- Set up the Jetson AGX Xavier (See setup guide) and make sure it is set to power mode "MAXN" for maximum performance and power usage.
- Plug the power cable into the Xavier, attach USB-C to the front port and click the left power button to turn it on.


## New Project

1. Set up project directory and virtual Python environment on Xavier
    1. SSH into jetson unit `ssh nvidia@192.168.55.1`
    2. Create project directory `mkdir projectName`, and `cd projectName`
    3. Create virtualenv 
        1. `sudo apt install python3-venv`
        2. `python3 -m venv env`
2. Create a new project with remote interpreter
    1. Create new project
    2. Choose project location
    3. Expand "Python Interpreter"
        1. Choose "Existing interpreter"
        2. Click on "..."
        3. Choose "SSH Interpreter"
        4. Enter host IP and username (192.168.55.1 and nvidia)
        5. Click next. If Connection Failed, click "Previous" and "Next" again
        6. Enter password or SSH key, click "Next"
        7. Choose the virtualenv interpreter `/home/nvidia/projectName/env/bin/python3`, click "Finish"
    4. "Remote project location" `/home/nvidia/projectName`
    5. Click "Create"
3. Change deployment configuration
    1. Open the "Remote Host" panel on the right
    2. Click on "..." to open "Deployment"
    3. In the menu on the right, right click the selected configuration and "Rename" it to the project name. Click "OK"
    3. In the "Connections" tab, set "Root path" to `/home/nvidia/projectName`
    4. In the "Mappings" tab, set "Deployment path" to `/`
    5. Click "OK"
4. (Optional) Configure synchronization
        1. In "Remote Host", to unsync files/folders, right click and "Exclude path"
        2. To force synchronization, right click and select "Sync With Local..."
        3. Click the "Synchronize All" arrows


## Existing Project
To set up remote interpreter with an existing project, follow steps 1, 3 and 4 in the guide above, but instead of creating a new project in step 2, do the following:

2. Change interpreter for existing project
    1. Open File > Settings
    2. In the menu on the left, select "Project: projectName" and click "Python Interpreter"
    3. Click the gear on the right > "Add..."
        1. Choose "SSH Interpreter"
        2. Enter host IP and username (192.168.55.1 and nvidia)
        3. Click next. If Connection Failed, click "Previous" and "Next" again
        4. Enter password or SSH key, click "Next"
        5. Choose the virtualenv interpreter `/home/nvidia/projectName/env/bin/python3`, click "Finish"
    4. "Remote project location" `/home/nvidia/projectName`
    5. Click "Create"