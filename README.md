# v-server-setup
Readme Descritpion of V-Server-Setup Project 

1. Login to your VServer with your Username and passwort: 
    ssh username@ip-adress 

2. if there are function of login with Username and passwort, logout from your VServer. 

3. Create SSH-Keys with Sandard ed22591 on your local maschine. 
    Use: ssh-keygen -t ed25519 -C "deine-email@example.com"

4. Use "type" on your local maschine to copy your generated public key on your VServer: 
    Use: type C:/Path/to/key| ssh username@ip-adress "cat >> /home/user/.ssh/authorized_keys"

5. Try to login to your VServer with your copied public key. The system dont ask you for a passwort. 
    ssh -i C:/Path1/to/key usernema@ipadress

6. Logout from your VServer and repeat Step 5. 
    Make sure that you can login with your SSH Key! 

7. Deatkivate Password Login. 
    1. Go to "etc/ssh/sshd.config" with Bash "sudo nano /etc/ssh/sshd_config"
    2. Serarch to "#PasswortAuthentication yes" and change it to "PasswortAuthentication no"
    3. Save the file and exit 
    4. Restart the sshd service with "sudo sysrtemctl restart ssh.service" 


8. Logut form Server 

9. Try Login with username and passwort like at stap 1. You must get a "Percession denied" 

10. Login with SSH to your VServer. 

11. Update Respoitories on your Server. 
    Use: "sudo apt update" 


12. Install Nginx on your Server.
    Use: "sudo apt install nginx -y"

13. Crearte Alternative html side for your nginx Serrver: 
    1. Create a new Directory with "mkdir /var/www/alternatvies" 
    2. Create a new HTML file with "sudo touch /var/www/alternatives/alternate-index.html"
    3. Add a new configuration to: "sudo nano /etc/nginx/sites-enabled/alternatives"
        1. Open File
        2. Add: 
            server {
            listen 8081;
            listen [::]:8081;

            root /var/www/alternatives;
            index alternate-index.html;

            location / {
                try_files $uri $uri/ =404;
            }
        3. Save this file and close it. 
    4. Open the new html file with "sudo nano var/www/alternatives/alternate-index.html"
    5. Take your HTML Code into this file. 
    6. Save and Close this file. 
    7. Open your new Websiete on "your-ip-adress:8081"