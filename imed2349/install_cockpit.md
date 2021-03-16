# Monitor the Server

To help us monitor the server, we are going to install Cockpit, a popular dashboard view of our server.  To do this, run the command `sudo apt install cockpit -y`

Next, we need to add a new firewall rule to allow the service to run on port 9090.  To do this, run the command `sudo ufw allow 9090/tcp`

Then using Firefox (you can also use Safari on Mac), replace YOUR_IP_ADDRESS with the IP address of your virtual machine and go to YOUR_IP_ADDRESS:9090  You will need to accept the security risks involved with the self-signed certificate (it is safe, since this is a local web server that isn't accessible from outside of your network).  You won't be able to do this using Chrome, Opera, or Edge.

You will be faced with a login screen.  Enter your Ubuntu username and password and login.  This will allow you to see different resources that are currently being used by the server, view the server logs, and more.  Take a few minutes to click through and familiarize yourself with the dashboard.