# vServer Settup

## Table of Contents

1. [Introduction](#Introduction)
2. [Prerequisites](#Prerequisites)
3. [Usage](#Usage)  
   - [Create SSH Keys](#Crearte-SSH-Keyws)  
   - [First Login with Passwort](#Login-wiith-Passwort)  
   - [Deactivate Passwort Login](#Deactivae-Passwortlogin)  
   - [Install nginx](#Install-Nginx)  
     - [Installing Process](#Installing-Process)  
     - [Create Alternative Website for nginx](#Create-alternatvie-Webseite)  


## Introduction
Readme Descritpion of V-Server-Setup Project. 
This Project describes how do you can set SSH Connection to your Server and configurate a nginx Webserver to this VServer. 

## Prerequisites: 
    You need a Ubuntu Cloud VM to setting your VServer.


## Usage 

### Create-SSH-Keys
1. Create SSH-Keys with Sandard ed22591 on your local maschine. 
    ``` bash
    ssh-keygen -t ed25519 -C "deine-email@example.com"
    ```


### Login-with-Passwort
2. Login to your VServer with your Username and passwort: 
    ```bash
    ssh <username>@<ip-adress> 
    ```

### Deacitvate-Passwortlogin
3. Use "type" on your local maschine to copy your generated public key on your VServer: 
    ``` bash
    type C:/Path/to/key| ssh username@ip-adress "cat >> /home/user/.ssh/authorized_keys"
    ```

4. Try to login to your VServer with your copied public key.
    ```bash
    ssh -i C:/Path1/to/key <usernema>@<ip-adress>
    ```

5. Deatkivate Password Login. 
    1. Go to "etc/ssh/sshd.config" with Bash 
    ``` bash
    sudo nano /etc/ssh/sshd_config
    ```
    2. Serarch to "#PasswortAuthentication yes" and change it to "PasswortAuthentication no"
    3. Save the file and exit 
    4. Restart the sshd service. 
    ``` bash
    sudo sysrtemctl restart ssh.service" 
    ```
### Install Nginx
#### Insalling--Process 

6. Update Respoitories on your Server. 
    ``` bash
    sudo apt update" 
    ```

7. Install Nginx on your Server.
    Use the following command: 
    ``` bash 
    sudo apt install nginx -y
    ```
#### Create-alternatvie-Webseite
8. Crearte Alternative html side for your nginx Serrver: 
    1. Create a new Directory 
    ``` bash
    mkdir -p /var/www/alternatives
    ```
    2. Create a new HTML file:
    ``` bash 
    sudo touch /var/www/alternatives/alternate-index.html
     ```
 
    3. Add a new configuration to: 
    ``` bash
    sudo nano /etc/nginx/sites-enabled/alternatives
    ```
        1. Open File
        2. Add: 
            ``` bash
            server {
            listen 8081;
            listen [::]:8081;

            root /var/www/alternatives;
            index alternate-index.html;git 

            location / {
                try_files $uri $uri/ =404;
            }
            ```
        3. Save this file and close it. 
    4. Open the new html file.
    ``` bash 
    sudo nano var/www/alternatives/alternate-index.html
    ```
    5. Take your HTML Code into this file. 
    6. Save and Close this file. 
    7. Open your new Websiete on "<your_ip>:8081"    


    Link zum dso-github: https://github.com/Developer-Akademie-GmbH/dso-python-tasks/pull/5
