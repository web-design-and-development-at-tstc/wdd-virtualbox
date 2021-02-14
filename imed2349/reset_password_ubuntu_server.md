# Reset Password for Ubuntu Server

If you find yourself in the situation where you are not able to remember your password you created for your user on Ubuntu Server, follow the steps below to reset the password.  You will have to perform these steps directly on the VM itself, you won't be able to perform these steps via SSH.

With your VM powered off, click the start button.  As your machine powers up, you'll see the boot screen.

![Ubuntu Server VM Boot Screen](https://inspiringweb.org/vm_images/VM_Boot_Screen.png)

As soon as you see the boot screen, push and hold the left Shift key until you see the screen below.

![Ubuntu Server GRUB Option Screen](https://inspiringweb.org/vm_images/Ubuntu_GRUB_Screen.png)

Use the arrow keys to navigate down to the option, "Advanced options for Ubuntu" and then hit enter.  You'll see two options for Ubuntu, one without the phrase "(recovery mode)" at the end and one that does end with the phrase "(recovery mode).

![Ubuntu Server Recovery Mode Options](https://inspiringweb.org/vm_images/Ubuntu_Recovery_Mode_Options.png)

Use the arrow keys to navigate down to the the Ubuntu option that ends with the phrase "(recovery mode)" and then hit enter.  This will load the Ubuntu Server in recovery mode.  The boot process is finished when you see the screen below.

![Ubuntu Server Recovery Menu options](https://inspiringweb.org/vm_images/Ubuntu_Recovery_Menu.png)

Using the arrow keys, navigate down to the root option and hit enter.

![Ubuntu Server root option](https://inspiringweb.org/vm_images/Ubuntu_root_option.png)

When you see the message "Press Enter for maintenance", hit enter again.

![Ubuntu Server root user CLI](https://inspiringweb.org/vm_images/Ubuntu_root_user_CLI.png)

Once you see the CLI with the command line beginning with root@HOST_NAME (where HOST_NAME is the name you gave the Ubuntu Server when you created your profile during the installation process).  You are currently in a read-only file system, so we have to remount the filesystem with write permissions.  To do this, run the command `mount -o remount,rw /`  Notice you don't need sudo for this command because we are already running as the root user on the systems.

Next, we will use the passwd command to reset the password for a specific user.  Run the command `passwd USERNAME` replacing the word USERNAME with the username you created and are wanting to reset the password for.  It will then ask you to "Enter new UNIX password:", enter your new password here making sure you only use the number row at the top of the keyboard and not the 10-key number pad.  Remember you won't see any characters on the screen.  After you hit enter, you'll see the message "Retype new UNIX password:" and you will need to re-enter the password again.  Once you have entered it a second time and hit enter, you will get the message "passwd: password updated successfully".

Once you have successfully reset the password, run the command `shutdown -r now` to reboot the server.  When the Ubuntu Server reboots and you reach the login screen, enter your username and the new password.
