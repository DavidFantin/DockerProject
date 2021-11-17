# Docker Project [CS-3353]
## Setting up docker
*Note: I used an Ubuntu VM with VMware, keeping the settings as default*
1. Update Ubuntu packages:
  - Command: sudo apt update
2. Install Docker:
  - Command: sudo apt install docker.io

## Installing OpenVAS via Docker

1. Grab the container "mikesplain/openvas" from the docker registry and launch it from port 443 (for https support in a web browser).
  - Note: I also added '$(pwd)/data:/var/lib/openvas/mgr/' to allow for volume support.
    - Command: sudo docker run -d -p 443:443 -v $(pwd)/data:/var/lib/openvas/mgr/ --name openvas mikesplain/openvas
2. Check out the web UI in a browser
  - Website to goto: https://localhost
  - Default login info:
      - Username: admin
      - Password: admin

## Creating the docker-compose.yml file from thr docker run command

1. Goto https://www.composerize.com/ (courtesy of Codi)
2. Copy and paste your Docker run command for setting up OpenVAS (mine was: -d -p 443:443 -v $(pwd)/data:/var/lib/openvas/mgr/ --name openvas mikesplain/openvas)
3. Create a new file called docker-compose.yml and copy the results from the website into it
4. To test it works:
    - Delete your current container
    - Run the command: sudo docker-compose up

## Run a vulnerability scan using OpenVAS

### Create and configure a target:
1. Under the "Configuration" tab in the top menu select "Targets"
2. Click the blue star icon at the top left of the screen (to create an new target)
    - Name the target (I named mine "target-1")
    - Set the target IP host, which is the IP address for target-1 (I used my laptop's wlan IPv4 address for this example)
    - Create the target

### Create and configure a scan task:
1. Under the "Scans" tab in the top menu select"Tasks"
2. Hover over the blue star icon at the top left of the screen and select ‘New Task’
    - Name the task (I named mine "scan_target-1")
    - Select "target-1" for the field:  "Scan Targets"
    - Tick the "once" checkbox for the "Schedule" field
    - Create the task
    
### Run the scan:
1. Click the start button next to the task
2. Click the green refresh button in the top right corner
    - Wait...

## Useful Docker commands I used:
1. Kill a container
  - Command: sudo docker kill [[containerName]]
2. Delete all contaners (that are not running)
  - Command: sudo docker system prune -a



sudo docker top openvas


sudo docker exec -it openvas bash

https://localhost/
