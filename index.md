# Docker Project: Install WordPress via Docker

Resources:

https://linuxiac.com/wordpress-with-docker/


## Step 1: Install Docker

Run the following two commands:

    sudo apt update
    sudo apt install docker.io
    
Notes: 
The first command updates apt, so it is pulling the latest installs from the apt repository.
The second command installs docker from the apt repository.


## Step 2: Install Docker Compose

First, install curl with the following command:

    sudo apt install curl
  

So, what is curl? Well, I'm glad you asked. Curl is a command line tool to transfer data to or from a server. We will be using it to install Docker Compose from Github. Docker Compose is a tool that was developed to help define and share multi-container applications.

Next, run the following commands to install docker-compose:

    sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    
After docker-compose is finished installing, run the following command to check the installation is successful and the version.

    docker-compose –version
    
Here is what my result looked like after running the command:

![Book logo](/DockerProject.io/Picture1.png)
