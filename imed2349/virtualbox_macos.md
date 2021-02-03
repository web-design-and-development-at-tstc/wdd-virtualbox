# VirtualBox Installation Guide

[VirtualBox](https://www.virtualbox.org/) is a powerful x86 and AMD64/Intel64 virtualization product for enterprise as well as home use. Not only is VirtualBox an extremely feature rich, high performance product for enterprise customers, it is also the only professional solution that is freely available as Open Source Software under the terms of the GNU General Public License (GPL) version 2. --VirtualBox.Org

## Download VirtualBox

To download VirtualBox, go to [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) and click on the **OS X Hosts** link located under the VirtualBox platform packages heading.  This will initiate the download of the .dmg file.

### Firefox Download

If you are using Firefox, you will get a dialog box asking "What should Firefox do with this file?"  Make sure the Save File radio button is selected and click OK.  This will save the .dmg file directly to your Mac Downloads folder.

<div style="text-align: center;">![Firefox Download Dialog Box](https://inspiringweb.org/vm_images/Firefox_Download_Dialog.png)</div>

### Chrome Download

If you are using Chrome, the download will start automatically and the .dmg file will save directly to your Mac Downloads folder.

### Safari Download

If your are using Safari, you will get a dialog box asking 'Do you want to allow downloads on "www.virtualbox.org"?'  Click Allow and the .dmg file will save directly to your Mac Downloads folder.

<div style="text-align: center;">![Safari Allow Download Dialog Box](https://inspiringweb.org/vm_images/Safari_Allow_Downloads_Dialog.png)</div>

## Install VirtualBox

Once the download is completed, you are ready to begin the installation process of VirtualBox.  Open the .dmg file in your Downloads folder and after a few seconds of processing, the installation screen will appear.  Double click on the icon under the number 1.

<div style="text-align: center;">![VirtualBox Installation Screen](https://inspiringweb.org/vm_images/VirtualBox_macOS_Installation_Screen.png)</div>

This will open up the package installer.  Depending on your macOS version, you should see a message that "This package will run a program to determine if the software can be installed".  Click Allow.

<div style="text-align: center;">![macOS Allow package to run program to determine if the software can be insalled dialog box](https://inspiringweb.org/vm_images/macOS_Allow_Dialog.png)</div>

Once the previous message box goes away, you will be on the Introduction screen for the VirtualBox installer.  Click Continue.

<div style="text-align: center;">![VirtualBox Installer Introduction Screen](https://inspiringweb.org/vm_images/macOS_Installer_Intro.png)</div>

Next, you'll be on the Installation Type screen for the installer.  To perform the standard installation (which is sufficient for our class), click Install.

<div style="text-align: center;">![VirtualBox Installer Installation Type Screen](https://inspiringweb.org/vm_images/macOS_Installer_Installation_Type.png)</div>

The macOS will ask for an administrator password (image not shown),  enter it and click OK.

This will initiate the installation process for VirtualBox.

<div style="text-align: center;">![VirtualBox Installer Installation Screen](https://inspiringweb.org/vm_images/macOS_Installer_Installation.png)</div>

Near the end of the process, you might get a message "A reboot is required...", click Ok.

<div style="text-align: center;">![macOS Reboot required dialog box](https://inspiringweb.org/vm_images/macOS_Reboot_Dialog.png)</div>

The installation process will finish. and you will see "The installation was successful." message.  Once you see that message, click Close.

<div style="text-align: center;">![VirtualBox Installation Success Screen](https://inspiringweb.org/vm_images/macOS_installation_Success_Screen.png)</div>

The installer will ask if you want to Keep the install file or move it to the trash.  If you try to move it to the trash, the process will fail.  So choose Keep, and you can move the file to the trash later.

<div style="text-align: center;">![macOS move installer to trash dialog box](https://inspiringweb.org/vm_images/macOS_Move_to_Trash.png)</div>

Once the installation is complete, restart your Mac.

## Open VirtualBox

After your system has restarted, to open VirtualBox either go to Applications and scrolldown to VirtualBox and double-click to open the app.  Alternatively, you can go to your Launchpad and search for VirtualBox and click on it to open the app.

Either option will open the Oracle VM VirtualBox Manager screen.

<div style="text-align: center;">![VirtualBox Manager Screen](https://inspiringweb.org/vm_images/VirtualBox_Manager_Screen.png)</div>

## Creating a Virtual Machine (VM)

Click on **Machine -> New** or click the **New** starburst button.

<div style="text-align: center;">![VirtualBox Machine -> New Menu](https://inspiringweb.org/vm_images/macOS_Machine_New.png)</div>

This will open the Name and operating system dialog box.  Enter a name for the VM.  I recommend the name of the OS and version number of the OS this VM will be running.  Under Type, make sure the correct OS Type is selected (ex. Linux if you are going to use Ubuntu Server) is selected and under Version, make sure the right bit version is selected (ex. Ubuntu (64-bit) if you are running Ubuntu Server).

<div style="text-align: center;">![VirtualBox Name and operating system dialog box](https://inspiringweb.org/vm_images/macOS_Name_OS_Dialog.png)</div>

Once you have adjusted these settings, click Continue.

Next you'll see the Memory size dialog box.  The Memory size is the amount of memory the Virtual Machine will have access to. This uses your host machine’s memory capacity. It is not recommended to use the maximum. For a computer that has 8GB of RAM, you could possibly afford to use 4GB for your Virtual Machine. Keep in mind that 1024 MB is 1 GB.  If at all possible, I wouldn't go below 4GB for the memory size.  After adjusting the memory, click Continue.

<div style="text-align: center;">![VirtualBox Memory size dialog box](https://inspiringweb.org/vm_images/macOS_Memory_Size.png)</div>

Next you'll see the Hard disk dialog box. Make sure the radio button for "Create a virtual hard disk now" is selected, then click Create.

<div style="text-align: center;">![VirtualBox Hard disk dialog box](https://inspiringweb.org/vm_images/macOS_Hard_Disk.png)</div>

Then you'll see the Hard disk file type dialog box.  Make sure the radio button for "VDI (VirtualBox Disk Image)" is selected, then click Continue.

<div style="text-align: center;">![VirtualBox Hard disk file type dialog box](https://inspiringweb.org/vm_images/macOS_Hard_Disk_File_Type.png)</div>

Next you'll see the Storage on physical hard disk dialog box.  It is asking you to choose between **Dynamically allocated** or **Fixed size** hard drive capacity for the Virtual Machine. Fixed size will be faster, but will use whatever value for your hard drive space as literal space on your host machine. Dynamically allocated space however, will start small and grow to the maximum capacity you set.  Once you have selected your option, click Continue.

<div style="text-align: center;">![VirtualBox Storage on physical hard drive dialog box](https://inspiringweb.org/vm_images/macOS_Storage_on_physical_hard_disk.png)</div>

Now you'll see the File location and size dialog box.  Keep the default file location.  In terms of the size, at a minimum, set this to 25 GB, but if you can go larger, go with 50 GB.  After you have set the size of the virtual hard disk, click Create.

<div style="text-align: center;">![VirtualBox File location and size dialog box](https://inspiringweb.org/vm_images/macOS_File_location_and_size.png)</div>

VirtualBox will finish creating the virtual machine and will display it in the VirtualBox Manager window when it is created.  Please note that this Virtual Machine is an empty shell. It does not have an operating system on it. You will need an ISO to install the OS on the VM.

<div style="text-align: center;">![VirtualBox File location and size dialog box](https://inspiringweb.org/vm_images/macOS_Ubuntu_VM.png)</div>

## Virtual Machine Settings

Before you install an OS, it is important to adjust the Network settings on this VM so it is able to connect to the Internet and so we can SSH remote into the machine and load websites off the VM. Select the VM you want to adjust, then click **File -> Host Network Manager**.

<div style="text-align: center;">![VirtualBox File -> Host Network Manager file menu](https://inspiringweb.org/vm_images/File_Host_Network_Manager_Menu.png)</div>

This will open up the Host Network Manager Screen.

<div style="text-align: center;">![Host network manager screen](https://inspiringweb.org/vm_images/Host_Network_Manager_Screen.png)</div>

Click the Create button and VirtualBox will automatically create a network with the name vboxnet0 with an IPv4 Address/Mask.  Make sure to check the checkbox next to Enable for the DHCP Server and then click the Close button.

<div style="text-align: center;">![Create host network dialog box - Create](https://inspiringweb.org/vm_images/Host_Network_Manager_Screen_Create.png)</div>

Next, make sure you have the VM selected and click on Settings (Yellow Gear Icon).  Then go to the Network tab.

<div style="text-align: center;">![Virtual Machine Settings Screen]()</div>

On Adapter 1, make sure the Attached to: drop down menu is set to NAT.

<div style="text-align: center;">![Network Setting Screen for Adapter 1](https://inspiringweb.org/vm_images/Network_Adapter_1.png)</div>

Then click on Adapter 2.  Click the checkbox for Enable Network Adapter.  Than in the Attached to: drop down menu, choose Host-only Adapter.  For the Name: drop down menu, make sure vboxnet0 is chosen.  Then click OK.

<div style="text-align: center;">![Network Setting Screen for Adapter 2](https://inspiringweb.org/vm_images/Network_Adapter_2.png)</div>

## Installing an Operating System

Select the VM and then click Start (green right arrow).

Upon starting the VM for the first time only, you’ll get a Select start-up disk dialog. Click Cancel.

<div style="text-align: center;">![VirtualBox select optical disk file dialog box](https://inspiringweb.org/vm_images/macOS_Choose_disk_image_dialog.png)</div>

This will open up the blank shell of your virtual machine.

On the bottom bar, click on the faded out disk icon and select "Choose a disk file"

<div style="text-align: center; margin-bottom: 2em;">![VM Choose a disk file icon](https://inspiringweb.org/vm_images/macOS_faded_disk_icon.png)</div>

<div style="text-align: center;">![VM Choose a disk file menu](https://inspiringweb.org/vm_images/macOS_Choose_a_disk.png)</div>

This will open up a window where you can navigate to the folder where your ISO file is located and select the ISO.  Click Open.

<div style="text-align: center;">![VM Choose a disk file finder](https://inspiringweb.org/vm_images/macOS_Choose_a_disk_finder.png)</div>

The disk icon should now be unfaded.  To start the installation process, click on **Machine -> Reset**.

<div style="text-align: center;">![VirtualBox Machine -> Reset Menu](https://inspiringweb.org/vm_images/macOS_Machine_Reset.png)</div>

Then on the dialog box asking "Do you really want to reset the following virtual machines?" click Reset.

<div style="text-align: center;">![VirtualBox Reboot Confirmation dialog box](https://inspiringweb.org/vm_images/macOS_Reset_Confirmation.png)</div>

This will initiate the installation process of the selected OS.

If the screen size is too small for you to read what is happening, click on the icon in the bottom bar that looks like a computer monitor.  Hover over Virtual Screen 1 and then click on "Scale to 200% (autoscaled output)".

<div style="text-align: center;">![VM Adjust Virtual Screen Size Menu](https://inspiringweb.org/vm_images/macOS_Virtual_Machine_Scale.png)</div>

Follow the prompts to install the OS.