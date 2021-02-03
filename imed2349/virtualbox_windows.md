# VirtualBox Installation Guide - Windows

[VirtualBox](https://www.virtualbox.org/) is a powerful x86 and AMD64/Intel64 virtualization product for enterprise as well as home use. Not only is VirtualBox an extremely feature rich, high performance product for enterprise customers, it is also the only professional solution that is freely available as Open Source Software under the terms of the GNU General Public License (GPL) version 2. --VirtualBox.Org

## Download VirtualBox

To download VirtualBox, go to [https://www.virtualbox.org/wiki/Downloads](https://www.virtualbox.org/wiki/Downloads) and click on the **Windows Hosts** link located under the VirtualBox platform packages heading.  This will initiate the download of the .exe file.

### Firefox Download

If you are using Firefox, you will get a dialog box asking "Would you like to save this file?"  Click the Save File button.  This will save the .exe file to your dsignated downloads folder.

![Firefox Download Dialog Box](https://inspiringweb.org/vm_images/Firefox_Download_Dialog.png)

### Chrome Download

If you are using Chrome, the download will start automatically and the .exe file will save directly to your users Downloads folder (or your defined downloads folder if set differently).

### Edge Download

If you are using Microsoft Edge, the download will start automatically and the .exe file will save directly to your users Downloads folder (or your defined downloads folder if set differently).

## Install VirtualBox

Once the download is completed, you are ready to begin the installation process of VirtualBox.  Open the .exe file in your Downloads folder and after a few seconds of processing, the installation screen will appear.  Click Next to get started with the installation process.

![VirtualBox Installation Screen]()

The next screen will allow you to determine what features are installed.  Leave the default settings as they are and click Next.

![VirtualBox Custom Setup Screen]()

Next, you'll see a screen with four checkboxes that are all checked.  Leave them checked and click Next.

![VirtualBox Custom Setup Options Screen]()

The next screen contains a Warning about VirtualBox installing a networking feature that will reset your network connection and temporarily disconnect you from the network.  This is temporary and your network connection will be restored.  Click Yes to proceed.

![VirtualBox Warning: Network Interfaces Screen]()

You are now ready to install VirtualBox.  Click Install to begin the installation.  

This will initiate the installation process for VirtualBox.

![VirtualBox Ready to Install Screen]()

If you are running a version of Windows with User Access Control, you will get a message asking "Do you want to allow this app to make changes to your device? Oracle VM VirtualBox... Click Yes and your installation will continue.

Next, you'll get a message asking "Would you like to install this device software?" to install USB drivers for the VM with a checkbox option for "Always trust software from "Oracle Corporation".  It is your choice whether to have that checkbox checked or not.  After you make that choice, click the Install button.

![Install USB Drivers Install Screen]()

If you unchecked the checkbox on the previous message, you'll get another message asking the same question but this time to install Network adapters along with that checkbox choice.  After you decide whether to have the checkbox checked, click the Install button.

![Install Network adapters Install Screen]()

Then, if you unchecked the checkbox on the previous message, you'll get a message asking the same question but this time to install Network Service.  After you decide whether to have the checkbox checked, click the Install button.

![Install Network Service Install Screen]()

The installation process will finish. and you will see "Oracle VM VirtualBox installation is complete" message.  Keep the checkbox to start VirtualBox after installation checked and click Finish.

![VirtualBox Installation Success Screen]()

## Open VirtualBox

If you kept the checkbox checked on the last screen, VirtualBox will automatically open.  In the future, to open VirtualBox click on the Desktop shortcut Oracle VM Virtual Box.

![VirtualBox Manager Screen]()

## Creating a Virtual Machine (VM)

Click on **Machine -> New** or click the **New** starburst button.

![VirtualBox Machine -> New Menu]()

This will open the Name and operating system dialog box.  Enter a name for the VM.  I recommend the name of the OS and version number of the OS this VM will be running.  Under Type, make sure the correct OS Type is selected (ex. Linux if you are going to use Ubuntu Server) is selected and under Version, make sure the right bit version is selected (ex. Ubuntu (64-bit) if you are running Ubuntu Server).

![VirtualBox Name and operating system dialog box]()

Once you have adjusted these settings, click Next.

Next you'll see the Memory size dialog box.  The Memory size is the amount of memory the Virtual Machine will have access to. This uses your host machine’s memory capacity. It is not recommended to use the maximum. For a computer that has 8GB of RAM, you could possibly afford to use 4GB for your Virtual Machine. Keep in mind that 1024 MB is 1 GB.  If at all possible, I wouldn't go below 4GB for the memory size.  After adjusting the memory, click Next.

![VirtualBox Memory size dialog box]()

Next you'll see the Hard disk dialog box. Make sure the radio button for "Create a virtual hard disk now" is selected, then click Create.

![VirtualBox Hard disk dialog box]()

Then you'll see the Hard disk file type dialog box.  Make sure the radio button for "VDI (VirtualBox Disk Image)" is selected, then click Next.

![VirtualBox Hard disk file type dialog box]()

Next you'll see the Storage on physical hard disk dialog box.  It is asking you to choose between **Dynamically allocated** or **Fixed size** hard drive capacity for the Virtual Machine. Fixed size will be faster, but will use whatever value for your hard drive space as literal space on your host machine. Dynamically allocated space however, will start small and grow to the maximum capacity you set.  Once you have selected your option, click Next.

![VirtualBox Storage on physical hard drive dialog box]()

Now you'll see the File location and size dialog box.  Keep the default file location.  In terms of the size, at a minimum, set this to 25 GB, but if you can go larger, go with 50 GB.  After you have set the size of the virtual hard disk, click Create.

![VirtualBox File location and size dialog box]()

VirtualBox will finish creating the virtual machine and will display it in the VirtualBox Manager window when it is created.  Please note that this Virtual Machine is an empty shell. It does not have an operating system on it. You will need an ISO to install the OS on the VM.

![VirtualBox Manager showing Ubuntu Server VM]()

## Virtual Machine Settings

Before you install an OS, it is important to adjust the Network settings on this VM so it is able to connect to the Internet and so we can SSH remote into the machine and load websites off the VM. Select the VM you want to adjust, then click **File -> Host Network Manager**.

![VirtualBox File -> Host Network Manager file menu]()

This will open up the Host Network Manager Screen.

You should have a Host named VirtualBox Host-Only Ethernet Adapter with an IPv4 Address/Mask and the checkbox next to Enable for the DHCP Server checked.  You might also have a second VirtualBox Host-Only Ethernet Adapter with a different IPv4 Address/Mask value and the checkbox next to Enable for the DHCP Server unchecked.  Make a note of the adapter that has the checked checkbox for enable, because that is the one you will want to use in a couple minutes.

Click on the adapter that has the Enable checkbox checked and then click on the Properties button.  Under the Adapter tab, click on the radio button for "Configure Adapter Automatically" and then click on the Apply button.  After it has been applied, click on the Close button.

![VirtualBox Host Network Manager Properties Screen]()

If you don't see these, click the Create button and VirtualBox will automatically create a host-only network with an IPv4 Address/Mask.  Make sure to check the checkbox next to Enable for the DHCP Server and then click the Close button.

![Create host network dialog box - Create]()

Next, make sure you have the VM selected and click on Settings (Yellow Gear Icon).  Then go to the Network tab.

On Adapter 1, make sure the Attached to: drop down menu is set to NAT.

![Network Setting Screen for Adapter 1]()

Then click on Adapter 2.  Click the checkbox for Enable Network Adapter.  Than in the Attached to: drop down menu, choose Host-only Adapter.  For the Name: drop down menu, make sure VirtualBox Host-Only Ethernet Adapter is chosen (if there were two listed on the Host Network Manager screen, make sure you choose the one that had the Enable checkbox checked for DHCP server).  Then click OK.

![Network Setting Screen for Adapter 2]()

## Installing an Operating System

Select the VM and then click Start (green right arrow).

Upon starting the VM for the first time only, you’ll get a Select start-up disk dialog. Click the folder icon.

![VirtualBox select optical disk file dialog box]()

This will open up the Optical Disk Selector Screen.  Click the Add button (a CD-ROM image with a plus sign).

![VM Optical Disk Selector Screen]()

This will open up a window where you can navigate to the folder where your ISO file is located and select the ISO.  Click Open.

![VM Choose a disk file window]()

Once you are back on the Optical Disk Selector screen, the ISO should be listed under Name.  If so, click the Choose button.

![VM Optical Disk Selector showing choosen ISO]()

This will take you back to the Select start-up disk dialog and the ISO choosen should be listed in the drop-down menu.  Make sure it is selected and then click the Start button.

![VirtualBox select optical disk file dialog box showing choosen ISO]()

This will initiate the installation process of the selected OS.

Follow the prompts to install the OS.