###### *The following is copied from [here](http://thisdavej.com/beginners-guide-to-installing-node-js-on-a-raspberry-pi) for safekeeping. All credit and many thanks to Dave Johnson ([@thisDaveJ](https://twitter.com/thisDaveJ)).*

TODO: Update the rest and images.

# Beginner’s Guide to Installing Node.js on a Raspberry Pi

##### This article has been updated to cover the installation of the latest version of Node at the time of this writing which is Node 7.x.

In this installment of our LTM (Learning through Making) series of Node.js tutorials, we’re going to get Node up and running on a Raspberry Pi 3 or Pi 2. With the Raspberry Pi 3, you won’t need to buy a separate USB Wi-Fi adapter. I’m focusing on the Raspberry Pi 3/Pi 2 rather than older versions such as the Raspberry Pi B+ since these are the latest models at the time of this writing.  The Raspberry Pi 3, for example, sports a 1.2 GHz quad-core ARMv8 chip with 1 GB of RAM versus the Raspberry Pi 1 Model B+’s 700 MHz single-core ARMv6 chip with 512 MB RAM.

The instructions provided here are for installing Node.js on a Pi 3 (ARMv8) or Pi 2 (ARMv7) rather than other models based on the ARMv6 chip such as the Raspberry Pi 1 Model B, Raspberry Pi Model B+ or the Raspberry Pi Zero.  A majority of this installation guide should still prove useful for other Raspberry Pi systems besides the Pi 3 and Pi 2; however, the final steps focused on the installation of Node.js will not work for these systems based on the older ARMv6 architecture.

This tutorial is useful for anyone wishing to successfully install a Raspberry Pi 3/Pi 2 system, even if they are not interested in Node.js since the Node.js installation happens in the final steps of the tutorial.  But, why would you not want to install Node.js? 🙂  Let’s get started!

### Hardware Needed
If you don’t currently own a Raspberry Pi, the easiest way to get started is to buy a starter kit such as this one on Amazon:
* [CanaKit Raspberry Pi 3 Complete Starter Kit – 32 GB Edition](https://www.amazon.com/gp/product/B01C6Q2GSY/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=B01C6Q2GSY&linkCode=as2&tag=thisdavej-20&linkId=VRAGHJ2RQIMQQTVG) (Note: my affiliate info is included on Amazon links so you can, if you desire, support these tutorials while paying nothing extra.)

We’ll need the following items to get rolling:
* Raspberry Pi 3 Model B or Pi 2 Model B  (these are the official names for the Raspberry Pi 3 and Pi 2.  **Don’t let the “B” confuse you since there is also an older Raspberry Pi Model B which is now effectively the “Raspberry Pi 1 Model B”.)**
* MicroSD card (I recommend a class 10 card that is 16 GB or higher.  I like this Samsung 32GB Class 10 microSD card.)
* MicroSD to SD memory card adapter (so you can use the SD card reader on your laptop/desktop to write to the microSD card.  Many microSD card vendors include this SD adapter with the purchase as shown here.)
<img src="http://thisdavej.com/wp-content/uploads/2016/02/SD-card-adapter.jpg"><br>
* Micro USB power supply (2.5A or greater recommended) to power the RasPi.
* (RasPi 2 only) USB WiFi adapter (or Ethernet cable if preferred.  I have tested this Edimax USB WiFi adapter on Raspbian and it works great out of the box.  There’s a reason this is a best seller on Amazon.)  This is not needed for the RasPi 3 since it includes built-in Wi-Fi.
* Windows laptop/desktop (Linux or Mac works great too, but this tutorial is geared more toward Windows machines so some readers will need to adapt)
* HDMI monitor/USB keyboard/mouse (You can borrow these from another system temporarily and then run your RasPi in a headless mode as I will explain later.)

### Write Raspbian Image to SD Card
We will be running Raspbian which is a free operating system based on Debian Linux and optimized for the RasPi.  Here we go:
* Download the latest Raspbian image from https://www.raspberrypi.org/downloads/raspbian/.  Be sure to download the full version rather than the “lite” version.  The download is a zip file that is about 1.5 GB so it may take some time to download depending on the speed of your Internet connection.
* Insert the microSD card into the SD adapter as shown in the Samsung sample picture above.
* Insert the SD adapter in the SD card reader on your laptop/desktop.  Make sure it is seated well in the connection.
*Launch Windows Explorer and verify that the SD card registers as a drive on your system.  Make a note of the drive letter as you will need it soon.
* Download and install Etcher.  Etcher is a cross-platform (Windows, OS X, Linux) tool for flashing images to SD cards.  It has many nice features including a simple user interface, the ability to flash an image without unzipping the zip file, and a validation step to verify the SD card image was written correctly to the SD card.
  * (As an alternative for Windows users, you can use Win32 Disk Imager since it also provides the ability to read an SD card and create an image file which is handy for creating snapshots of Raspberry Pi systems that can flashed back to an SD card later if needed.  For Win32 Disk Imager, you will need to first unzip the downloaded zip file before burning the .img file to the appropriate drive letter containing your SD card.)
* Launch Etcher.  Be patient as Etcher takes a number of seconds to launch.  When launched, the interface will look something like this:
<img src="http://thisdavej.com/wp-content/uploads/2016/06/etcher1.png"><br>
* Click the Select image button and navigate to the Raspbian zip file that you downloaded.  (It does NOT need to be unzipped before flashing.)
* Click the Select drive button to specify the target device location of the SD card.
WARNING: Be sure you choose the right target device or you will write the image to another drive on your system and this will not be good.
* Click the Flash! button to write the image to your SD card.
* If you are running Windows,  you may be presented with a security prompt regarding making changes to your device. If so, click Yes to proceed.
* After the image is written to the SD card and verified, Etcher will automatically dismount your SD card so it can be safely removed.
* Remove the SD adapter from your laptop/desktop, and remove the microSD card from the SD adapter.

### Prep the Hardware
The [Tech Brick Café](http://techbrickcafe.blogspot.com/2015/10/raspberry-pi-2-model-b-single-board.html) has a nice overview picture of the various parts of the RasPi 2 [here](http://1.bp.blogspot.com/-v9M2cZM4BJo/Vi4l_fie0sI/AAAAAAAAAAw/9aa1y3-hhVQ/s400/Raspberry_pi_2_2.PNG) (RasPi 3 looks very similar) that may help you in this section.  Let’s get this little SBC (single board computer) ready to boot! Here are the steps:
* Insert the microSD card into the RasPi.  (Turn the RasPi upside down.  The microSD card slot is located on the side opposite of the USB ports.  This short video explains the process well.)
* Connect the USB keyboard and mouse
* Connect the HDMI cable
* Connect the USB Wi-Fi adapter (or Ethernet connection if you are not using Wi-Fi)  This step is not necessary if you are using a Raspberry Pi 3 which has on-board Wi-Fi.
* Connect the power supply (You will see the RasPi lights come on and power up.)
* You should now see Raspbian booting on the screen.  Hooray!

### Configure the RasPi
We first need to make a few changes to the RasPi to for the purpose of optimization and personalizing it for our use.  To get started, launch Raspberry Pi Configuration which is located in the Menu under Preferences.
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rc_gui.png"><br>
This will launch the Raspberry Pi Configuration utility, a handy graphical version of the console-based raspi-config program that was used for many years to configure the RasPi (and is actually still used behind the scenes by this graphical version).  This will launch the following window:
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rcg1.png"><br>
Let’s start configuring!
* Expand Filesystem – click this button to expand the filesystem.  This ensures that all of the SD card storage is available to Raspbian.
* (Optional) Change Password – from a security perspective, it’s a good idea to change the default password for the “pi” user.  Just make sure you don’t forget it. 😉
* Hostname – if you prefer less typing when connecting remotely (explained later), you can change the host name from “raspberrypi” to something shorter such as “raspi”.

### Localization
The Raspberry Pi is the brilliant brainchild from our friends in the UK.  If you are not from the UK, you will need to change some of the localization settings.  For example, some of the keys on your keyboard may not work as expected.  Here are the changes I made to make my RasPi feel at home in San Diego:

First, click on the Localisation tab:
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rcg2.png"><br>
Click the Set Locale button to change your locale as appropriate and then click OK.  Mine looks like this after making the changes:
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rcg3.png"><br>
Click the Set Timezone button to set your timezone and then click OK.
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rcg4-1.png"><br>
Click the Set Keyboard button to set your keyboard as appropriate and then click OK.  Here’s mine:
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rc_keyboard.png"><br>
Finally, click the Set WiFi Country button and change as needed.  This dialog box presents a large list of countries. Use the arrow keys on your keyboard to scroll through the list to find your country and then click OK.
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/wifi-country.png"><br>
After completing these configuration steps, click OK to exit the Raspberry Pi Configuration program.  The RasPi will then let you know that it needs to reboot to activate the changes you just made.  Reboot it now.

### Configure Wi-Fi
After the RasPi reboots, we are ready to get Wi-Fi up and running to get on the network.

* Click on the network icon in the top right of the screen as shown in the screenshot. The network icon will look different than the icon in the screenshot before Wi-Fi is configured; however, it will should be located between the Bluetooth icon and the speaker (volume control) icon.
<br><img scr="http://thisdavej.com/wp-content/uploads/2016/06/wifi.png"><br>
* After clicking the network icon, select your network SSID (Wi-Fi network).  If you don’t see your Wi-Fi network, be patient. You may see a “Scanning APs” message in the menu; however, your Wi-Fi network SSID should eventually appear in the menu after it is located.  When your network SSID appears, click on it.
* You will be prompted for your pre shared key (Wi-Fi) network password.  Enter it and select OK.
* Wait for the icon to transform from a network icon to the Wi-Fi icon shown in the screenshot above.  From this point, you should be connected to your Wi-Fi network.
* Test your Wi-Fi network connection by launching the terminal.
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/terminal.png"><br>
* From the terminal, issue a ping command to verify your network connection is working:<br>
`$ ping google.com`

We’re now ready to move on and ensure our system is up to date with security patches.

### Apply Raspbian Updates
We will first run the apt “update” command.  This command will not actually update any software on the system, but will download the latest package lists from the software repositories so that Raspbian will be aware of all new software available along with dependencies.  Issue the following command at the “$” prompt:
<br>`$ sudo apt update`<br>
Next, run the following command to upgrade any packages installed on your system that need upgrades:
<br>`$ sudo apt full-upgrade`<br>
This is important to keep your RasPi system synchronized with security updates, etc. These two commands should be issued together and run periodically.

### Prepare Remote Desktop
We want to run our RasPi remotely without requiring a dedicated HDMI monitor and USB keyboard/mouse.  This is known as headless mode. We will be using the xrdp package to accomplish this goal. Newer versions of Raspbian (starting with versions that ship with the PIXEL desktop environment) ship with RealVNC for remote connections.  Unfortunately, RealVNC does not work well in headless mode since it degrades to a very low resolution, and there is quite a bit of ceremony required to change the resolution. The xrdp solution automatically scales our desktop resolution and makes our life much easier.  Let’s do it:
* Before we can install xrdp, we must first install the tightvncserver package.  The tightvncserver installation will also remove the RealVNC server software that ships with newer versions of Raspbian since tightvncserver (xrdp) will not work if RealVNC is installed.  (Thanks to Ryan Hanley for this tip!) Enter the following command in the terminal:
<br>`$ sudo apt install -y tightvncserver`<br>
The “-y” option will automatically answer yes to the default questions which is what we want in this context.
* Next, invoke the following command to install xrdp:
<br>`$ sudo apt install -y xrdp`<br>
* Finally, we need to install the samba package so we will be able to access the RasPi by its host name from Windows machines on the network rather than by it’s IP address which can change since the RasPi receives its IP address via DHCP.  (For OS X users, you can install Bonjour and then access your Raspberry Pi by host name.  For example, if your host name is “raspi”, you can access it on OS X as “raspi.local”.)  OK, let’s install Samba:
<br>`$ sudo apt install -y samba`<br>
* After this installation completes, you should be able to ping the RasPi Hostname (configured in Raspberry Pi Configuration program above) from a Windows machine:
<br>`C:\> ping raspi`<br>
* You are now ready to launch a remote desktop connection!
* From your Windows machine, hit the Windows key, and type “Remote Desktop Connection” to bring up the Remote Desktop program.  Click it in to invoke it.  (OS X users can use Microsoft Remote Desktop which is available for free in the Mac App Store.)
* Type the host name of your RasPi (“raspi” in my case) in the Computer textbox.<br>
<img src="http://thisdavej.com/wp-content/uploads/2016/06/rdp.png"><br>
* Next, click the Display tab. Move the Display configuration slider all the way to the right to “Full Screen” to ensure our remote desktop connection will fill our screen.  It may already be set to “Full Screen”.
<br><img src="http://thisdavej.com/wp-content/uploads/2016/06/rdp2.png"><br>
* Click the Connect button near the bottom of the dialog box.
* You will then be prompted with the xrdp login screen:
<br><img src="http://thisdavej.com/wp-content/uploads/2016/02/xrdpLogin.png"><br>
* Enter your credentials and log into the RasPi.
  * username: pi
  * password: raspberry (unless you changed it in the Raspberry Pi Configuration program earlier in the tutorial.)
  
Amazing!  We are connected remotely to the RasPi and we no longer need the dedicated HDMI monitor and USB keyboard/mouse. Let’s go ahead and shut down the RasPi for a minute so we can free up our monitor and keyboard/mouse:

* Launch a terminal session and enter the following command to cleanly shut down your system:
<br>`$ sudo poweroff`<br>
* Wait a minute for the RasPi to fully power down.
* Unplug the power cable, HDMI cable, and the USB keyboard and mouse.
* Plug the power cable back in and the RasPi should be on its way back up without all of those extra cables!
* After giving the RasPi a minute or so to boot, connect to it once again using the Windows Remote Desktop program.
