# Setting Up Virtual Hosts

With Apache, it is possible to host multiple sites/domains on Apache using Virtual Hosts.  Even if you are only going to host a single site/domain, it is still a good idea to set up a directory and Virtual Host. If you ever decide to add another domain later, things will be a lot easier for you.  For this guide, we are not going to use registered domains and we'll set up the hosts file in our OS to resolve the domains we use in this guide.

The first domain we are going to make a virtual host for is `jdoe.test` (where j is the initial of your first name and doe is your last name; so for example my first domain would be `dtrower.test`).  The second domain we are going to make a virtual host for is a development domain for your food truck/restaurant.  In this guide, replace `jdoe.test` with the domain using your name and replace `food_truck.test` with a development domain for your food truck/restaurant.  You don't want to use the actual domain that you plan to register, because of the changes we will be making to the host file during this process.

## Create Directories and Set Permissions

Inside the `/var/www/` directory we are going to create two new directories for our two domains.  Remember to replace `jdoe.test` and `food_truck.test` with your own development domains.

Run the command `sudo mkdir -p /var/www/jdoe.test/public_html`

Then run the command `sudo mkdir -p /var/www/food_truck.test/public_html`

## Create Test Web Pages

For each domain we are going to create a simple index.html web page to test that our setup is correct.  Remember to replace `jdoe.test` and `food_truck.test` with your own development domains.

To create the first index.html web page for `jdoe.test`, run the command `sudo nano /var/www/jdoe.test/public_html/index.html`

In the nano editor, Create a simple HTML web page with the your name in the &lt;title&gt; element and inside an &lt;h1&gt; element so we can see something in the tab and the browser window when we load the website.

To exit the nano editor and save this file, press CTRL+X to exit, type `Y` to save, and Enter to confirm the file name.

We'll do the same thing for food_truck.test.  Run the command `sudo nano /var/www/food_truck.test/public_html/index.html`

In the nano editor, Create a simple HTML web page with the name of your food truck/restaurant in the &lt;title&gt; element and inside an &lt;h1&gt; element so we can see something in the tab and the browser window when we load the website.

To exit the nano editor and save this file, press CTRL+X to exit, type `Y` to save, and Enter to confirm the file name.

Since the commands executed above were done as a sudo user, the newly created files are owned by root.  We'll want to avoid any permission issues by changing the ownership of the domain document root directory and all files contained within to the apache user (www-data).  To do this, run the command `sudo chown -R www-data: /var/www/jdoe.test` and then run the command `sudo chown -R www-data: /var/www/food_truck.test`.

## Create New Virtual Host Files

The Virtual Host files are used to tell Apache how to respond to various domain requests.   These files are located in `/etc/apache2/sites-available`.

To create a virtual hosts configuration file, run the command `sudo nano /etc/apache2/sites-available/jdoe.test.conf`

Enter the information below making sure to replace each instance of jdoe.test with your personal test domain (there are seven occurences of the domain name).  You should be able to use the keyboard copy and paste commands to copy the block of directives below and paste it into your CLI while you are in the nano editor so you don't have to try and write it all out.  However, if you aren't able to copy/paste double check your work before you save and proceed with the setup of virtual hosts.

~~~
<VirtualHost *:80>
    ServerName jdoe.test
    ServerAlias www.jdoe.test
    ServerAdmin webmaster@jdoe.test
    DocumentRoot /var/www/jdoe.test/public_html
  
    <Directory /var/www/jdoe.test/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
  
    ErrorLog ${APACHE_LOG_DIR}/jdoe.test-error.log
    CustomLog ${APACHE_LOG_DIR}/jdoe.test-access.log combined
</VirtualHost>
~~~

Save and close nano by pressing Ctrl+X, then type `Y` and hit Enter.

We'll create another virtual hosts configuration file for our food truck/restraunt.  Run the command `sudo nano /etc/apache2/sites-available/food_truck.test.conf`

Enter the information below making sure to replace each instance of food_truck.test with your personal test domain (there are seven occurences of the domain name).

```
<VirtualHost *:80>
    ServerName food_truck.test
    ServerAlias www.food_truck.test
    ServerAdmin webmaster@food_truck.test
    DocumentRoot /var/www/food_truck.test/public_html
    
    <Directory /var/www/food_truck.test/public_html>
        Options -Indexes +FollowSymLinks
        AllowOverride All
    </Directory>
  
    ErrorLog ${APACHE_LOG_DIR}/food_truck.test-error.log
    CustomLog ${APACHE_LOG_DIR}/food_truck.test-access.log combined
</VirtualHost>
```
Save and close nano by pressing Ctrl+X, then type `Y` and hit Enter.

## Enable New Virtual Host files

Now that we have the two virtual host files in place, we need to enable them.  Remember to replace the domains below with your own domains.

First, run the command `sudo a2ensite jdoe.test.conf`  You should see the following message:

```shell
  Enabling site jdoe.test.
  To activate the new configuration, you need to run:
    systemctl reload apache2
```

Next, run the command `sudo a2ensite food_truck.test.conf`  You should see the following message:

```shell
  Enabling site food_truck.test.
  To activate the new configuration, you need to run:
    systemctl reload apache2
```  

Before we restart the server, we'll test the configuration syntax for errors.  To do this, run the command `apachectl configtest`  You can safely ignore any errors that say "Could not reliably determine the server's fully qualified domain name".  As long as you see `Syntax OK`, it is time to restart Apache.

To restart Apache, run the command `sudo systemctl reload apache2`

## Edit Host file

If this were a live web server and you used domain names that you have registered, you would need to point your domains to the IP of your Apache server so they can be served across the Internet.  Since we are using development domains, we need to edit the hosts file on our computer to point to these domains on our Apache Server.  Find the relevant guide below based on the OS you are running.

### macOS

To edit the hosts file on a Mac, open a new Terminal window and run the command `sudo nano /etc/hosts`  You will need to enter your administrator password to be able to open and edit this file.

Once the hosts file is open, enter the following two lines into the file replacing the `IP_ADDRESS` with the IP address of your virutal machine web server and the domains with your own domains.

```shell
  IP_ADDRESS jdoe.test
  IP_ADDRESS food_truck.test
```

Save and close the file by pressing Ctrl+X, type `Y`, and hit Enter.

Then run the command, `sudo dscacheutil -flushcache`

### Windows 8/10

Click on the Start windows icon to open the menu and type `Notepad`.

Right click on __Notepad__ and choose __Run as administrator__. If you are prompted for an administrator password or for a confirmation, type the password and click __Allow__ or __Yes__.

In Notepad, click __File__ and __Open__ then navigate to the hosts file.  The file is located in `C:\Windows\System32\drivers\etc`.  If the folder appears blank, click on the file extension dropdown where it says __Text Documents (*.txt)__ and change it to __All Files (*.*)__.

Open the file called __hosts__.

Once the hosts file is open, enter the following two lines into the file replacing the `IP_ADDRESS` with the IP address of your virtual machine web server and the domains with your own domains.

```shell
  IP_ADDRESS jdoe.test
  IP_ADDRESS food_truck.test
```

Once you have made the necessary changes, click __File__ and __Save__.

### Windows Vista/7

Click Start windows icon.  Then, click __All Programs__.  Next, click __Accessories__.  Finally, right-click on __Notepad__ and then click __Run as administrator__. If you are prompted for an administrator password or for a confirmation, type the password of click __Allow__ or __Yes__.

In Notepad, click __File__ and __Open__ then navigate to the hosts file.  The file is located in `C:\Windows\System32\drivers\etc`.  If the folder appears blank, click on the file extension dropdown where it says __Text Documents (*.txt)__ and change it to __All Files (*.*)__.

Open the file called __hosts__.

Once the hosts file is open, enter the following two lines into the file replacing the `IP_ADDRESS` with the IP address of your virtual machine web server and the domains with your own domains.

```shell
  IP_ADDRESS jdoe.test
  IP_ADDRESS food_truck.test
```

Once you have made the necessary changes, click __File__ and __Save__.

## Test Virutal Hosts

Once you have enabled the hosts files on the VM Ubuntu Server and edited your hosts file on your personal Mac or Windows computer, it is time to test if your server and host files are working as intended.

Open your preferred browser and enter into the address bar `jdoe.test` and hit enter.  You should see your name displayed in both the Tab and in the browser viewport.

Repeat with entering into the address bar `food_truck.test` and hit Enter.  You should see the name of your food truck/restraunt in the Tab and in the browser viewport.

If you both sites load as intended, great job!  You just installed and set up a fully functioning web server.