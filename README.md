# HP-8570p-Hackintosh-Master
HP EliteBook 8570p Hackintosh Files and Guide

// Information
- Easy step by step setup with Windows
- No knowledge of DSDT/SSDT patching needed

// What you need
- A PC with Windows installed. 
- USB 2.0 drive with a minimal storage of 16 GB
- The pre-installation and post-installation files from my GitHub
- Internet connection to your laptop with a ethernet cable

// Links
- GitHub https://github.com/AlphaGoob/HP-8570p-Hackintosh-Master
- Troubleshooting: https://github.com/AlphaGoob/HP-8570p-Hackintosh-Archive
- Catalina recovery (if GibMacOS is not working) https://drive.google.com/file/d/1m-9geijbYCML29jd5gOn39br-cK8xmv0

// My specifications
- HP EliteBook 8570p
- Intel core i5 3210M (Ivy Bridge)
- Intel HD 4000
- Intel 7 series chipset
- Intel 82579L ethernet
- Intel Centrino Ultimate-N 6300 AGN (633ANHMW)
- Audio IDT Codec (Layout-ID 2)
- SSD (multiple brands possible)

// Tested on
- macOS 10.13 High Sierra
- macOS 10.14 Mojave
- macOS 10.15 Catalina

// What works:
- Keyboard and trackpad
- Audio (speakers and microphone)
- USB ports
- Camera
- Battery status
- Graphics
- Ethernet
- iCloud (App store, iMessage and FaceTime) and Airplay

// Not Working:
- WiFi 
- Bluetooth

# Before starting

// Notes:
I’m not a experienced hackintosh-er. I assume the SSDT’s, DSDT’s and config files can be done better, but it all works very stable. If you have any suggestion or adjustments please contact me. I would be glad to change and test it out. 

// Tips:
- Use a USB mouse at the catalina installer. Your trackpad will be very slow. It is solved in the post-installation.
- Boot the installation of macOS in Verbose mode. The loading bar will sometimes not move but in verbose you will see all progress. Do this by pressing the space bar in Clover on you macOS Installation and select Verbose. 
- If you don’t have another drive to boot (for example Windows) you can setup Clover Configurator so it doesn’t show the selection screen. For that go to Boot option in Clover Configurator and select “Fast”. 

# Pre-installation

BIOS Settings 
Update your BIOS to the latest version
Open your BIOS settings with F10
Restore your BIOS defaults
Check the following settings:
Boot settings - Custom Logo [Optional for Apple logo at boot]
Boot settings - Disable fast boot
Boot settings - Boot mode - UEFI hybrid (with CSM)
Boot settings - Disable Secure boot (disabled if greyed out)
Device configuration - Disable Wake on USB
Built-in Device Options - Disable LAN/WLAN switching
Built-in Device Options - Wake on LAN - Disable
Port Options - Disable serial port
Port Options - Disable 1394 port

Making a USB installation
Install Python and don’t forget to select “Add python to path” in the installer
Open GibMacOS (gibmacos.bat) as administrator
Select recovery mode with “R”
Select the option for Catalina with “full install” in the note
GibMacOS will create some folders, open them until you see a .pkg file
Copy the path of the PKG file
Insert your USB Stick at a usb port on your motherboard
In this case it are the USB ports under your power button.
Open GibMacOS (makeinstall.bat) as administrator
Select your USB drive with the corresponding number
If the installer ask for your recovery path paste it here (pkg of step 6)
Note: This can take up to 15 minutes

Preparing the USB drive
Delete all files in the following folders on your USB drive
/EFI/BOOT/BOOTX64.efi
/EFI/CLOVER/drivers/BIOS
/EFI/CLOVER/drivers/UEFI
/EFI/CLOVER/kexts/Other
Delete the CLOVERX64.efi and config.plist in your /EFI/CLOVER folder
Open Clover pre-installation folder
Copy /EFI/CLOVER/ACPI to the /EFI/CLOVER/ folder on your USB drive
Copy all files from the following folders in the pre-installation folder to your USB drive
/EFI/BOOT/
/EFI/CLOVER/drivers/BIOS
/EFI/CLOVER/drivers/UEFI
/EFI/CLOVER/kexts/Other
And finally copy CLOVERX64.EFI, config.plist and drivers64UEFI to the clover folder on your USB drive.
Check the Clover folder. You now should have a copy of my Clover folder (a full copy won’t work, that’s why i use all the steps)

Install MacOS Catalina
Restart your laptop
Press F9 for your boot menu
Select Boot from EFI file
Navigate to /EFI/BOOT/BOOTX64.efi
Select this option and Clover will load
In clover, hit Enter on MacOS recovery installation
In the MacOS Installation open Disk Utility
Remove all volumes on the Internal SSD
Select Container Disk1 and select Erase
Name your disk (i like “Hackintosh HD”)
Select APFS as structure, and click erase. 
Close the disk utility and open the MacOS Installer
Follow the instructions in the installer
Your laptop will reboot and show Clover again select the installer from your internal SSD instead of the USB Drive.
Note: This can take up to 30 minutes
If your laptop reboots for the second time and shows Clover select Boot macOS from internal HDD.
Note: This can take up to 10 minutes

# Post-installation

Clover Configurator
Go to Finder > Settings
Enable your hard drive to show on your desktop
Unzip Clover Configurator
Move Clover Configurator to your Apps folder on your hard drive

Setup your EFI disk
Open Clover Configurator
If you start Clover Configurator for the first time you need to go to Security in your settings panel and enable Clover to start. 
Click on Mount Efi and select Mount Partition. A Partition will show on your desktop
Rename the partitition to “HP_TOOLS” [HP Custom boot logo]
Move the Hewlett-Packard folder to your EFI partition [HP Custom boot logo]
Replace the EFI folder with the post-installation clover folder. 
If you don’t want to use my bootloader theme you can delete the bootcamp_alpha folder from /EFI/CLOVER/themes/

Make SMBios suitable for iCloud
Open Clover Configurator
Select File > Open and open the config.plist you just moved to your EFI/CLOVER/
Click on SMBIOS
Select “Generate New” under both System - Serial Number as System - SmUUID

Enable Audio
Install VoodooHDA
Click next until you see the screen “Installationtype” Now select “Edit” on the left. 
Unfold the first option (VoodooHDA Clover UEFI/ESP and select macOS Catalina. 
Click Install. You will get voodoohda.kext in your clover folder and a extra menu in your preferences.
Go to your system preferences
Select VoodooHDA
On the left select Microphone (Both)
Slide the Monitor slider all the way down.  

Disable hibernate (Your system will freeze at sleep otherwise)
Open up your terminal and run the following commands
sudo pmset -a hibernatemode 0
sudo rm /var/vm/sleepimage
sudo mkdir /var/vm/sleepimage

All Done! 
