## Install MySQL Server

To install the MySQL Server, type the command `sudo apt-get install mysql-server` and hit Enter.

If asked for your password, enter the password for your Ubuntu Server user.

Once it has identified everything needed to install, type `Y` and hit Enter.

## Secure MySQL Server

Once MySQL Server is installed, lets secure it. Type the command `sudo mysql_secure_installation` and hit Enter.

It will ask if you want to use the VALIDATE PASSWORD COMPONENT.  Type 'Y' and hit enter.

For our purposes, we are going to use the strong-level password policy. In development, you could get away with low or medium level for a password policy, but it's best to always be in the habit to use the strongest security available. Type `2` and hit Enter.

Enter a password for the root account for MySQL. Because we are using the strong level password policy we need to use special characters in addition to numbers and mixed case letters.  Make sure you keep track of this password. You will need to enter the password and hit enter. Please note that you won’t see anything on screen.

It will then ask you to re-enter the password. Enter the password a second time and hit enter. Just like the first time you entered the password, you will not see anything happening on screen.

It will then ask if you want to continue with the password provided. Type `Y` and hit Enter.

Next, it asks if you want to remove anonymous uses. Type `Y` and hit Enter.

The next question is related to using the root user remotely. Type `Y` and hit Enter.

Next it asks if you want to remove the test database.  Type `Y` and hit Enter.

The next question asks if you want to reload the privileges database. Type `Y` and hit Enter.

Next, type `sudo mysql` and hit enter.

Then type in the command `ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'YOUR_MYSQL_PASSWORD';` making sure to replace the words YOUR_MYSQL_PASSWORD with the password you just created and hit Enter.

After it has run, type `exit` and hit Enter.  This will exit you out of working on the MySQL Server and return you to working on the Ubuntu Server.

## Connect to MySQL Server

To connect to the MySQL Server via CLI, type the command `sudo mysql -u root -p` and hit enter.

It will then ask for the password.  Type in the MySQL password you created and hit enter (keep in mind you won't see characters on the screen as you type the password).

You are now logged into the MySQL Server via the CLI and can execute MySQL queries.  To log out of the MySQL Server, type `exit` and hit enter.