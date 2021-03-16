# Install phpMyAdmin on Ubuntu

The tool phpMyAdmin allows for easier MySQL/MariaDB database management.  As such, we'll install phpMyAdmin on our web server.

To begin, we are going to update the package lists by running the command `sudo apt update`

## Pre-Installation Preparation
Before we install phpMyAdmin, we are going to explicitly enable the mbstring PHP extension by running the command `sudo phpenmod mbstring` and then restarting Apache (`sudo systemctl restart apache2`).

We'll also be needing a package to unzip a zip file, so run the command `sudo apt install unzip`

Finally, later on we are going to need to generate a random password.  We are going to install the pwgen package by running the command `sudo apt install pwgen`

## Download the Source Files

While normally we would use the distribution packages in Ubuntu, this time we are going to download the source files directly from the company.  To find the latest stable version of phpMyAdmin, in a browser go to [phpMyAdmin](https://www.phpmyadmin.net/files/) and find the latest version number without any alpha or rc designations.  At the time of this guide, the current version is 5.1.0 which is what I'll be using in my commands.

We are going to download the zip file into the /tmp directory, so first we are going to navigate into that directory using the command `cd /tmp`

Now we are ready to download the zip file using wget.  Run the command `wget https://files.phpmyadmin.net/phpMyAdmin/5.1.0/phpMyAdmin-5.1.0-all-languages.zip`

Once it has finished downloading, we are ready to extract the zip.  Run the command `unzip phpMyAdmin-5.1.0-all-languages.zip`

After the unzipping is completed, we need to rename the folder by running the command `mv phpMyAdmin-1.1.0-all-languages phpmyadmin`

Next, we will move the renamed folder into our document root folder for our Apache web server (/var/www/html) by running the command `sudo mv phpmyadmin /var/www/html`

## Configure phpMyAdmin

Navigate to the phpmyadmin directory using the command `cd /var/www/html/phpmyadmin`

Next we'll rename the config.sample.inc.php file by running the command `sudo mv config.sample.inc.php config.inc.php`

## Create MySQL superuser for phpMyAdmin

Because we disabled remote login when we installed MySQL, we are going to create a superuser just for phpMyAdmin.

To create a superuser for just phpMyAdmin, log into MySQL as `root` using the command `sudo mysql -u root -p`

It will then ask for the password.  Enter the password you created when you set up your MySQL server. After you type it in, remember you won't see any characters on screen, hit Enter.

Next we are going to add a new MySQL user called `pmauser` (which stands for PHP My Admin User).  In a production environment, you would want your `root` MySQL user and your `pmauser` MySQL user to have different passwords, but for our purposes, you can use the password of your choice and in the following command replace YOUR_PASSWORD_HERE with the password you want to assign to the `pmauser` account.  TO create the user account, run the query `CREATE USER 'pmauser'@'%' IDENTIFIED BY 'YOUR_PASSWORD_HERE';`.  You should get the result:  
  `Query OK, 0 rows affected (0.00 sec)`

Then we'll grant superuser privileges to our new user `pmauser`.  To do this, run the command `GRANT ALL PRIVILEGES ON *.* TO 'pmauser'@'%' WITH GRANT OPTION;`.  You should see the result of this query as:  
  `Query OK, 0 rows affected (0.00 sec)`

Now exit MySQL.

## Test phpMyAdmin

Now, we should be able to access and log into the phpMyAdmin web interface.

- In your browser, enter your server's IP address followed by `/phpmyadmin`. e.g. `http://192.168.56.6/phpmyadmin`

- You should see the login form shown below.

![Login screen for phpMyAdmin](https://inspiringweb.org/vm_images/phpMyAdmin_login_screen.png)

- Enter the the MySQL user `pmauser` in the username field and then password you created in the password field then click __Go__.  Once you are logged in, you should see a screen similar to the one below.  At the bottom of the screen you might see a couple of red errors and one yellow warning.  We'll correct all of these over the next few minutes.

![Web Interface for phpMyAdmin with 2 red errors and 1 yellow warning](https://inspiringweb.org/vm_images/phpMyAdmin_errors_warnings.png)

First, in the warning message, click on the link "Find out why".

On the next page, you will see the some output followed by another warning message.

![Find out Why page showing output and warning message](https://inspiringweb.org/vm_images/phpMyAdmin_Create_phpmyadmin_db.png)

In the warning message, click on the link called "Create" which run the queries to create a database named phpmyadmin.

You'll see a bunch of outputted messages all with the green OK and Enabled.  As seen in the below screenshot.

![Output of phpmyadmin database creation](https://inspiringweb.org/vm_images/phpMyAdmin_database_creation.png)

To get back to our warnings, click on the home icon in the upper right in the sidebar.  The second error message is concerning a `tmp` directory not being accessible.  To resolve these, we are going to create a tmp directory inside the phpmyadmin folder (make sure you are still in the directory `/var/www/html/phpmyadmin` before running the `mkdir` command).  Run the command `mkdir tmp`

Next, we'll need to change the ownership of the folder to be that of our Apache user.  To do this, run the command `sudo chown www-date:www-data /var/www/html/phpmyadmin/tmp`

We are going to generate a random password to use for the blowfish-secret.  To generate a random password, run the command `pwgen -syn1 46` and ensure that there is not a single quote mark inside the password generated.  If there is, rerun the password generator to get a new unique password.

Highlight the randomly generated password and hit CMD+C or CTRL+C to copy the text.

Next, open up the file config.inc.php using the nano editor by running the command `sudo nano config.inc.php`

Find the line that begins with `$cfg['blowfish_secret']` and then using your cursor to navigate inside the single quote marks, hit CMD+V or CTRL+V to paste the random password into the PHP array.  Then press CTRL+X to exit, type `Y` to save the results, and then hit enter to save it to that file name.

When you refresh the page for phpMyAdmin in your browser, it will take you back to the login screen and you will need to re-log in with your pmauser username and password.  After you are logged in, both red errors and the yellow warning that were at the bottom of the screen should be gone.

Once we are finished, in our Terminal let's go back to our root folder by running the command `cd ~`