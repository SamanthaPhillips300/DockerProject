# Docker Project: Install WordPress via Docker

### Created by: Samantha Phillips

Resources:

[How to Install WordPress with Docker, An Easily to Follow Guide](https://linuxiac.com/wordpress-with-docker/)


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


![Example One](/docs/assets/images/Picture1.png)


## Step 3: Create a Directory

Create a directory to store the WordPress data:

     sudo mkdir -p /srv/wordpress
     cd /srv/wordpress
       
Example:

![Example Two](/docs/assets/images/Picture2.png)

## Step 4: Create the YAML File

Purpose: yaml file allows for the deployment, combination and configuration of multiple docker containers at the same time.

First, install vim (or another text editor)

     sudo apt install vim
        
Next, switch to the root user

     sudo -s
        
Now create a file called docker-compose.yaml using vim, so you will be able to instantly edit the file.

     vim docker-compose.yaml
        
Add the following to the docker-compose.yaml file:

     version: '3'
     services:
       mysql:
         image: mysql:latest
         restart: always
         environment:
           MYSQL_ROOT_PASSWORD: my_password
           MYSQL_DATABASE: wordpress
           MYSQL_USER: wordpress_user
           MYSQL_PASSWORD: wordpress_password
         volumes:
           - mysql_data:/var/lib/mysql
       wordpress:
         image: wordpress:latest
         depends_on:
           - mysql
         ports:
           - 8080:80
         restart: always
         environment:
           WORDPRESS_DB_HOST: mysql:3306
           WORDPRESS_DB_USER: wordpress_user
           WORDPRESS_DB_PASSWORD: wordpress_password
         volumes:
           - ./wp-content:/var/www/html/wp-content
     volumes:
       mysql_data:

 
To save and exit the file in vim press the "ESC" button and type :wq

Note: More information about the details in the .yaml file can be found in the resource link at the top of the page. In short, it will build two docker containers: a WordPress containter for the WordPress site and a MySQL container to store any data from the WordPress site. 

Check to make sure the file saved properly by running the following command:

    cat docker-compose.yaml
   
It should look similar to this:

![Example 3](/docs/assets/images/Picture03.png)

Lastly, exit out of the root user:

    exit
    
# Step 5: Install WordPress

Run the following command to use the .yaml file just created to build/install the WordPress image

    sudo docker-compose up -d
    
Once the command has finished running, WordPress is installed!!!

# Step 6: Access the WordPress Installation

In your web browser, navigate to http://localhost:8080 or http://your_ip_address:8080

This webpage will appear:

![Exampe Four](/docs/assets/images/Picture4.png)

Follow the insturctions to set up your account and then you will be ready to create a WordPress site!

# Appendix

## Screenshot of my WordPress Admin Interface

![WordPress Admin](/docs/assets/images/Picture6.png)

## Screenshot of the WordPress Page I made:

![WordPress Page](/docs/assets/images/Picture7.png)

This screenshot is from me accessing the webpage on my computer versus inside the VM :)
