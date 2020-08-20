# Pycharm remote interpreter

0. Create project on jetson
    1. SSH into jetson unit
    2. create project folder `mkdir projectName`, and `cd projectName`
    3. create virtualenv 
        1. sudo apt install python3-venv
        2. `python3 -m venv venv`

1. Create a new project
    1. Create new project
    2. Choose project location
    3. Expand "Python Interpreter"
        1. choose "Existing interpreter"
        2. click on "..."
        3. Choose "SSH Interpreter"
        4. Enter host IP and username (192.168.55.1 and nvidia)
        5. Click next. If Connection Failed, click "Previous" and "Next" again
        6. Enter password or SSH key, click "Next"
        7. Choose the virtualenv interpreter `/home/nvidia/projectName/venv/bin/python3`, click "Finish"
    4. "Remote project location" `/home/nvidia/projectName`
    5. Click "Create"

2. Change configuration
    1. Open the "Remote Host" panel on the right
    2. Click on "..." to open "Deployment"
    3. In the menu on the right, right click the selected configuration and "Rename" it to the project name. Click "OK"
    3. In the "Connections" tab, set "Root path" to `/home/nvidia/projectName`
    4. In the "Mappings" tab, set "Deployment path" to `/`
    5. Click "OK"

3. (Optional) Configure synchronization
    1. In "Remote Host", to unsync files/folders, right click and "Exclude path"
    2. To force synchronization, right click and select "Sync With Local..."
    3. Click the "Synchronize All" arrows
    

