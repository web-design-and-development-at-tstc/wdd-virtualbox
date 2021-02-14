# Install FTP Server

We are going to use the popular FTP server vsftpd (Very Secure File Transfer Protocol Daemon) for Ubuntu.

To begin, we are going to update the package lists by running the command `sudo apt update`

Next, we'll download and install vsftpd by running the command `sudo apt install vsftpd`.

Once it has installed, we can check the status to make sure vsftpd is running by running the command `sudo service vsftpd status`.  You should see a message similar to the one below if it is running correctly:

```shell
  ● vsftpd.service - vsftpd FTP server
       Loaded: loaded (/lib/systemd/system/vsftpd.service; enabled; vendor preset>
       Active: active (running) since Mon 2021-02-01 12:35:34 CST; 20s ago
     Main PID: 26269 (vsftpd)
        Tasks: 1 (limit: 4620)
       Memory: 588.0K
       CGroup: /system.slice/vsftpd.service
               └─26269 /usr/sbin/vsftpd /etc/vsftpd.conf

  Feb 01 12:35:34 ubuntu systemd[1]: Starting vsftpd FTP server...
  Feb 01 12:35:34 ubuntu systemd[1]: Started vsftpd FTP server.
```

## Create FTP User

To be able to log in to FTP, we need to create a user.

To create the user, `ftpuser` run the command `sudo adduser ftpuser`

It will ask you to enter new UNIX password.  Enter a password here, making sure to make note of it.  Like with other passwords, you won't see any characters on screen.  Once you have typed in the password, hit Enter.

It will then ask you to retype the password.  After you have retyped it, hit Enter.

Next, it will ask for some contact information (full name, room number, work phone, home phone, and other). You can leave these blank and just hit Enter for each value.

After the last value (other), it will ask `Is the information correct? [Y/n]`, type `Y` and hit Enter.

## Directory Permissions

Since we are going to be using our FTP server to transfer files to a web server, we'll set the home folder for the `ftpuser` to `/var/www/`.  This will allow the user to be able to upload to any site we host on our web server.  In this same way, if we were hosting multiple client websites and wanted to give each client access to just their website via FTP, we can follow these same steps and use a more specific home folder that limits their access to just their website.

To set the folder above the document root as the home directory for the `ftpuser`, run the command `sudo usermod -d /var/www ftpuser`

Next, we'll set the ownership of the document root directory to `ftpuser`.  This will allow our FTP user to  write and alter files in the document root directory.  To do this, run the command `sudo chown ftpuser:ftpuser /var/www/html`

## Configure vsftpd

Before we can start using FTP on our Ubuntu Server, there are a few changes we need to make to the vsftpd configuration file.

Before we edit the file, let's create a backup.  Run the command `sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.bak`

Next, open the configuration file in nano by running the command `sudo nano /etc/vsftpd.conf`

First, we'll allow FTP users to write files to the server. Press Ctrl+W and type `#write_enable`.  Then press Enter.  This will go to the place in the file where this directive is set.  Remove the pound sign (`#`) from the start of the line to uncomment the directive and make sure the directive is set to `YES`.

Next, we'll limit the FTP users from browsing outside their own directory.  Press Ctrl+W and type `#chroot_local_user`.  Then press Enter.  This will go to the place in the file where this directive is set.  Remove the pound sign (`#`) from the start of the line to uncomment the directive and make sure the directive is set to `YES`.

Then, we'll make sure uploaded files and folders are given the correct permissions. Press Ctrl+W and type `#local_umask`.  Then press Enter.  This will go to the place in the file where this directive is set.  Remove the pound sign (`#`) from the start of the file to uncomment the directive and make sure the directive is set to `022`.

The next two directives don't exist in the file so we are going to have to add them.  The first directive will force vsftpd to show file names that being with a dot, like `.htaccess`.  By default, Linux doesn't show these files and thus they won't be visible in FTP which is a problem if you intend to use Apache and work with `.htaccess`.

To force vsftpd to show file names that begin with a dot, move all the way to the bottom of the file and type in the directive `force_dot_files=YES`

Finally, we'll want to add some port ranges for passive FTP to make sure enough connections are available. Add these directive to the end of the file:  
  - `pasv_min_port=40000`  
  - `pasv_max_port=50000`

To save the file and exit nano, press Ctrl+X, then type `Y`, and hit Enter.

For these configuration changes to take effect, we need to restart the FTP server.  Run the command `sudo systemctl restart vsftpd`

## Test FTP

To make sure that our FTP server is working correctly, we are going to test vsftpd to see if we can log in with the user we created earlier.

Open up FileZilla and in the Quickconnect bar, enter your server's IP address for the Host, `ftpuser` for the username, and `WDDrules20` for the password (if you didn't use this one, then you should use the password you set when you created the `ftpuser` account).  Then click __Quickconnect__.

You'll get a dialog box that says "This server does not support FTP over TLS.  If you continue, your password and files will be sent in clear over the internet."  For now, click __OK__.  In the next unit of the course, we'll set up TLS on our server.

On the right hand side, you'll see that the only folder listed is the html folder which is located inside `/var/www`.  If you open this folder, you'll see an index.html file and the info.php file we created during the PHP installation.  Remember, anything you upload here will be live on your webserver.  Try uploading, creating, and editing folders and files within the web root directory (`/var/www/html`) to ensure permissions are working correctly.

Once you have finished testing, close your FileZilla.