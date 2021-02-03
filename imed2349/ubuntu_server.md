# Installing Ubuntu Server 20.04 LTS

## Download Ubuntu Server

Visit the [Get Ubuntu Server](https://ubuntu.com/download/server) and click on the button "Option 2 - Manual server installation".  A green button will appear above the option buttons where you can download the current LTS-supported version of Ubuntu Server, currently Ubuntu Server 20.04.1 LTS.  Click that button to initiate the download.

When running web servers, you don't want to be making major changes to your base OS to frequently, so it's best to pick a version that has long term support (LTS).  You'll notice that this version of Ubuntu Server will be supported until April of 2025.

Make sure you download this to your Downloads folder on the Mac.

## Install Ubuntu Server on VirtualBox

Follow the installation instructions in the VirtualBox Installation Guide to select the ISO for Ubuntu Server and initiate the installation process.

When it asks you to select your language use the up and down arrow keys and make sure English is selected.  Then hit Enter.

![Choose language screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Choose_Language.png)
 
If you get a message that an updated version of the installer is now avaialble, use the up and down arrow keys to select Update to the new installer, and hit Enter.

![Installer update available screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Update_Installer.png)
 
Next, it will ask you to select your keyboard layout.  It should default to English (US) and if it does, make sure Done is selected and hit Enter.

![Keyboard configuration screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Keyboard_Configuration.png)
 
Then, it will ask to configure at least one interface to talk to other machines.  Make sure that both enp0s3 and enp0s8 are listed with IP addresses.  Leave the defaults alone, make sure Done is selected, and hit Enter.

![Network connections screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Network_Connections.png)
 
Next, it will ask about proxy information, assuming you don't use a proxy, leave this blank, make sure Done is selected, and hit Enter.

![Configure proxy screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Proxy_Settings.png)
 
Next, it will ask about using an Ubuntu archive mirror.  It should default to the US mirror, so make sure Done is selected, and hit Enter.

![Configure Ubuntu archive mirror screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Configure_Mirror.png)
 
Then, it wil ask to configure a guided storage layout or create a custom one, leave the defaults selected, use the arrow keys to navigate to Done and then hit enter.

![Guided storage configuration screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Guided_Storage_Configuration.png)
 
Next, it will show a file system summary.  Make sure Done is selected and hit Enter.

![Storage configuration screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Storage_Configuration_Summary.png)

You'll get a message saying that selecting Continue will begin the installation process and result in the loss of data on the disks selected. You won't be losing any data on your host computer, the spaced used will be empty space on your hard drive.  Use the arrow key to select Continue and hit Enter.

![Confirm destructive action message during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Storage_Configuration_Dialog_Confirmation.png)

Next, it is going to ask you to enter your name, a server name, a username, and password to log into the system.  After you enter the information, use the arrow key to navigate to Done and hit Enter.

![Profile setup screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Profile_Setup.png)

Then, it is going to ask if you want to install OpenSSH server to allow remote access.  Press Enter to place an X to Install OpenSSH Server.  Then use the arrow keys to navigate to Done and hit Enter.

![SSH setup screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_SSH_Setup.png)

Next, it will ask if you want to install popular snaps.  Leave all of them unselected, navigate to Done and hit Enter.

![Featured Server Snaps screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Snaps_Setup.png)

The installation process will start and just let it run.

![Installing system screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Installing_System.png)

The installation is complete when you see a red banner at the top reading "Install complete!"  Using your arrows, navigate to Reboot Now and hit enter.

![Install complete! screen during Ubuntu Server 20.04 installation](https://inspiringweb.org/vm_images/Ubuntu_Install_Complete.png)

If you get a message about failed unmounting due to cdrom, go to **Machine -> Reset** and restart the VM.  You will see a bunch of text scrolling by as the server restarts.

![Failed unmounting /cdroom screen during Ubuntu Server 20.04 reboot](https://inspiringweb.org/vm_images/Failed_Unmounting_cdrom.png)

The reboot is finished when you see the line `[  OK  ] Reached target Cloud-init target.` and no more action is taking place on the screen.

![Finished reboot screen after Ubuntu Server 20.04 reboot](https://inspiringweb.org/vm_images/Ubuntu_SSH_Key.png)

Hit enter and the CLI will ask for your username.  Enter the username you created earlier than hit enter.  Next it will ask for your password.  Enter the password you created earlier.  Please note that you will not see any characters on screen while typing your password.

![Ubuntu login after Ubuntu Server 20.04 reboot](https://inspiringweb.org/vm_images/Ubuntu_Login.png)

## Set Timezone

Before moving on with updating and installing new packages, we need to set the timezone for our server.  This ensures that we are seeing the right date/time for where the server is being used.

To see what the timezone is currently set to, run the command `date`.  On a fresh install, the timezone defaults to UTC time.

Assuming you are located in the Central Standard Timezone, then you will want to use the timezone `America/Chicago`.  This way the server will automatically adjust for daylight savings time.  If you ever need to find a list of timezones, Run the command `timedatectl list-timezones` and navigate through the list to find a city in your timezone.  Once you have made a note of the exact timezone name, type `q` and hit enter.

To set the timezone, we are going to run the command `sudo timedatectl set-timezone America/Chicago`.  It will ask for the password for your account (as a reminder, anytime you enter your password in the CLI, you won't see any text or symbols on screen.  To confirm that the timezone has been changed, run the command `date` again and verify that it is showing CST/CDT (depending on if we are currently in daylight savings time or not) instead of UTC.

## Update Firmware

To update the firmware on the Ubuntu Server as well as any installed software, we will enter several commands in our Command Line.

Type `sudo apt-get update` into the Command Line and hit Enter

Once it has finished running, type `sudo apt-get upgrade -y` and hit Enter.

After it has run, type `sudo apt-get dist-upgrade -y` and hit Enter.

## Get IP Address

Next, we need to get the IP address for our virtual machine so we can remote into our Ubuntu Server VM.

Before we can get the IP address, we need to install some networking tools.  Type `sudo apt install net-tools` and hit Enter.

Once it has finished installing, to find the IP address for your virtual machine, type the command `ifconfig` and hit Enter.

This will print a bunch of information to the command line.  Assuming you set the Network Adapter 1 to NAT and Network Adapter 2 to Host-only Adapter and the name to vobxnet0, then to identify your IP address, look for the inet address under enp0s8.  The IP address you are needing should start with 192.168.  Make sure you write this IP address down because you will need it to connect to the Ubuntu Server VM from your host computer.

## Install Fail2Ban

Fail2Ban blocks suspicious requests that come from the Internet.  It will block the IP address if there are too many attempts to guess the password.

In the Terminal window, type `sudo apt-get install fail2ban`

It will download everything needed and then you will be asked if you want to continue.  Type `Y` and hit Enter.

After it has finished running, type `sudo systemctl enable fail2ban` and hit Enter.

After it has finished running, we need to set some settings for this.  To begin we are going to create a new file.  Type the command `sudo nano /etc/fail2ban/jail.local` and hit Enter.

In the editor, you will need to enter the following information:

```
  [DEFAULT]
  # Ban hosts for one hour:
  bantime = 3600

  # Override /etc/fail2ban/jail.d/00-firewalld.conf:
  banaction = iptables-multiport

  [sshd]
  enabled = true
```

To exit the nano editor and save this file, press CTRL+X to exit, type `Y` to save, and Enter to confirm the file name.

For these settings to take effect, we need to restart the fail2ban service.  To do this, type the command `sudo systemctl restart fail2ban` and hit Enter.

To verify that the service is running, we can use the fail2ban-client.  Type the command `sudo fail2ban-client status` and hit Enter.

You should see the output:

```
  Status
  |- Number of jail:      1
  `- Jail list:   sshd
```

## Shutdown and Reboot Ubuntu Server

To reboot the Ubuntu Server, type the command `sudo shutdown -r now` and hit enter.  The Ubuntu Server will reboot and you will be able to log in after it has finished rebooting.

To shutdown the Ubuntu Server and close the virtual machine, type the command `sudo shutdown now` and hit enter.  This will cause the Ubuntu Server to shutdown.  After the OS has shutdown, the virtual machine will automatically power off.