# Using SSH to Connect to Server Remotely - macOS

## Verify SSH Status

In this class, after the initial setup, we are going to remote into our VM.  You will only be able to remote into the VM while you are on the same network as the VM.

To verify that the SSH server is running, run the command `sudo systemctl status ssh`.  You should see in the output the message `Active: active (running)`.

## Connect to Virtual Machine using SSH

For the rest of the installation and setup process, you need to remote into your VM using an SSH client.  An SSH client is built into the macOS, so all you need to do is open up the Terminal window.  You do this by going to `Finder -> Applications -> Utilities -> Terminal`.

In the Terminal window, run the command `ssh USERNAME@IP_ADDRESS` where you will replace the word USERNAME with the username you created when you installed Ubuntu Server and the words IP_ADDRESS with the IP address you wrote down earlier and hit Enter.

The first time you try to connect to your VM remotely via the Terminal, you will get a message that the authenticity of host IP_ADDRESS can't be established and an ECDSA key fingerprint.  It will ask you if you want to continue connecting.  Type in `Yes` and hit Enter.

This will generate a warning that the IP_ADDRESS (ECSDA) has been permanently added to the list of known hosts and then will ask for your password.  Enter the password for the username on the VM not the password for your Mac (remember you won't be able to see any characters on screen as you enter the password).

You know you have been successfully connected to the remote Ubuntu Server when you see the message "Welcome to Ubuntu 20.04.2 LTS" along with additional information.  Your other visual clue that you are successfully connected is you Terminal window now shows the user as USERNAME@HOSTNAME (for example, jdtrower@ubuntu).  The hostname is the name of the server you created when you did the profile setup during the installation process.  The terminal also changes the color of a remote user to lime green whereas the local user is in white.  Now anything you do in the Terminal window until we exit will be performed on the Ubuntu Server running on the VM instead of on the Mac computer.

In subsequent times logging in remotely to the server, you will enter `ssh USERNAME@IP_ADDRESS` and hit enter and it will immediately ask for your password.  Enter the password for the user on the VM not for your Mac.

To end the remote connection, type the word `exit` in the Terminal window and hit enter.  You'll see the message similar to below upong successful logout:

```shell
  logout
  Connection to 192.168.56.4 closed.
```