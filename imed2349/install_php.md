# Install PHP Module

## Install Apache Utilities

First, we are going to make sure that some useful Apache utilities are installed.  Run the command, `sudo apt install apache2-utils software-properties-common`.  These may already be installed and at the latest version. If not, let them install before continuing.

## Add PHP and Apache2 PPA Repositories

We need to add a PPA repository to allow us to install the latest version of PHP.  To do this, run the command `sudo add-apt-repository ppa:ondrej/php`.  After it has begun to run, it will ask you to press Enter to continue or Ctrl+C to cancel adding it.  Hit Enter.

Next, we are going to add a PPA repository for apache 2.  Run the command `sudo add-apt-repository ppa:ondrej/apache2`.  After it has begun to run, it will ask you to press Enter to continue or Ctrl+C to cancel adding it.  Hit Enter.

After you have added both repositories, run the command `sudo apt-get update`.

## Install PHP

Now that we have the PPA repositories set up, we can install PHP 7.4 onto our web server.  To do this, run the command `sudo apt install php8.0 libapache2-mod-php8.0`.  When it asks if you want to continue, type `Y` and hit Enter.

When it has finished running, to verify that the installation was successful, run the command `php -v`.

If PHP was successfully installed, you will see output similar to:

```shell
  PHP 8.0.5 (cli) (built: May 3 2021 11:30:57) ( NTS )
  Copyright (c) The PHP Group
  Zend Engine v4.0.5, Copyright (c) Zend Technologies
      with Zend OPcache v8.0.5, Copyright (c), by Zend Technologies
```

Next, run the following command (while I have split the command onto multiple lines so it's viewable, you should enter it all as a single command without hitting enter until you are ready to execute the whole command):

```shell
sudo apt install php8.0-common php8.0-mysql php8.0-xml php8.0-xmlrpc php8.0-curl php8.0-gd php8.0-imagick
php8.0-cli php8.0-dev php8.0-imap php8.0-mbstring php8.0-opcache php8.0-soap php8.0-zip php8.0-intl
```

After it has determined what all will be installed, it will ask if you want to continue.  Type `Y` and hit Enter.

Finally, run the command `sudo apt-get upgrade -y`.

## Configure PHP

To get better performance out of our PHP module, we are going to update several values in the php.ini file.  To open the file, run the command `sudo nano /etc/php/8.0/apache2/php.ini`.

Press Ctrl+W and type `upload_max_filesize`.  Then press enter.  This will go to the place in the file where this variable is set.  Change its value to `32m`.

Press Ctrl+W and type `post_max_size`.  Then press enter.  This will go to the place in the file where this variable is set.  Change its value to `48M`.

Press Ctrl+W and type `memory_limit` .  Then press enter.  This will go to the place in the file where this variable is set.  Change its value to `256M`.

Press Ctrl+W and type `max_execution_time`.  Then press enter.  This will go to the place in the file where this variable is set.  Change its value to `600`.

Press Ctrl+W and type `max_input_vars`.  Then press enter.  This will go to the place in the file where this variable is set.  Remove the semi-colon (`;`) at the start of the line and change its value to `3000`.

Press Ctrl+W and type `max_input_time`.  Then press enter.  It will take you to the first instance which ins information about this setting.  Press Ctrl+W again and then hit Enter.  This will go to the place in the file where this variable is set.  Change its value to `1000`.

Once you have set all 6 of these settings, press Ctrl+X, then type `Y`, and then press Enter.

For these changes to take affect, run the command `sudo systemctl restart apache2.service`.

## Verify PHP is Working

In the Terminal window, run the command `sudo nano /var/www/html/info.php`

In the Nano editor, write the HTML code to create a basic HTML document and in the body of the web page include the PHP code, `<?php phpinfo(); ?>`

Once you are finished writing the code, press CTRL + X, then hit `Y`, and then enter.

Open up your browser and go to your IP_ADDRESS/info.php (make sure you replace the IP_ADDRESS with the IP address of your VM).  You should see the PHP Info page showing the version of PHP you have installed and a bunch of configuration information.