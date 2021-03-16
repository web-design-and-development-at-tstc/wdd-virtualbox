# Firewall Security

To help secure our web server, we are going a firewall on our server.  Before you start make sure you run the commands to update the firmware (`sudo apt-get update`, `sudo apt-get upgrade -y`, and `sudo apt-get dist-upgrade -y`).

## Configure Firewall

Before we enable the firewall, since we are actively using SSH to connect to our server remotely and don't want to lock ourselves out of the web server when we enable the firewall, we are going to add a rule for SSH.  Run the command `sudo ufw allow OpenSSH`.  You should see the following output:

```shell
   Rules updated
   Rules updated (v6)
```

If you got the message that rules updated, then we are ready to enable the firewall.  To do this, run the command `sudo ufw enable`

The terminal will display the message "Command may disrupt existing ssh connections. Proceed with operation (y|n)?" Type `Y` and hit Enter.

You should get the message, "Firewall is active and enabled on system startup".

You can check the current status of your firewall by running the command `sudo ufw status`.  Right now, the only rules you should see are the two for OpenSSH.  You can run this command at any point to see what rules you have enabled in your firewall.

## Configure Firewall for Apache, PHP, and MySQL

With your firewall enabled, try using your browser to navigate to your Apache configuration page (located at your VM IP address).  You'll see that your browser just hangs for a while before timing out.  This is because we have not opened the ports necessary to allow connections to our Apache server.

To add the firewall rules for Apache, run the command `sudo ufw allow in "Apache Full"`. You should get the output:

```shell
   Rules updated
   Rules updated (v6)
```

Reload your Apache configuration page and verify that you Apache server is now working as intended.

## Configure Firewall for FTP

If you were to try and connect to your server via FTP, the connection would be rejected by the server since we enabled the ufw firewall.  To fix this, we need to add some additional rules to open up the ports that are needed for FTP, ports 20 and 21 for FTP and ports 40000-50000 for passive FTP. We'll also open up port 990 for TLS.

First, run the command `sudo ufw allow 20/tcp`. You should get the output:

```shell
   Rules updated
   Rules updated (v6)
```

Next, run the command `sudo ufw allow 21/tcp`. You should get the output:

```shell
   Rules updated
   Rules updated (v6)
```

Then, run the command `sudo ufw allow 40000:50000/tcp`. You should get the output:

```shell
   Rules updated
   Rules updated (v6)
```

Finally, run the command `sudo ufw allow 990/tcp`. You should get the output:

```shell
   Rules updated
   Rules updated (v6)
```

You can check the current status of your firewall by running the command `sudo ufw status`. Provided you have been adding the rules as we have gone along, you should get the following status and list of active rules:

```shell
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
Apache Full                ALLOW       Anywhere
20/tcp                     ALLOW       Anywhere
21/tcp                     ALLOW       Anywhere
40000:50000/tcp            ALLOW       Anywhere
990/tcp                    ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
Apache Full (v6)           ALLOW       Anywhere (v6)
20/tcp (v6)                ALLOW       Anywhere (v6)
21/tcp (v6)                ALLOW       Anywhere (v6)
40000:50000/tcp (v6)       ALLOW       Anywhere (v6)
990/tcp (v6)               ALLOW       Anywhere (v6)
```