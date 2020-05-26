# HP-8570p-Hackintosh-Master
HP EliteBook 8570p Hackintosh Files and Guide

// Information:
- Easy step by step setup with Windows
- No knowledge of DSDT/SSDT patching needed

// What you need:
- A PC with Windows installed. 
- USB 2.0 drive with a minimal storage of 16 GB
- The pre-installation and post-installation files from my GitHub
- Internet connection to your laptop with a ethernet cable

// Links:
- GitHub https://github.com/AlphaGoob/HP-8570p-Hackintosh-Master
- Troubleshooting: https://github.com/AlphaGoob/HP-8570p-Hackintosh-Archive
- Catalina recovery (if GibMacOS is not working) https://drive.google.com/file/d/1m-9geijbYCML29jd5gOn39br-cK8xmv0

// My specifications:
- HP EliteBook 8570p
- Intel core i5 3210M (Ivy Bridge)
- Intel HD 4000
- Intel 7 series chipset
- Intel 82579L ethernet
- Intel Centrino Ultimate-N 6300 AGN (633ANHMW)
- Audio IDT Codec (Layout-ID 2)
- SSD (multiple brands possible)

// Tested on:
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
- I’m not a experienced hackintosh-er. I assume the SSDT’s, DSDT’s and config files can be done better, but it all works very stable. If you have any suggestion or adjustments please contact me. I would be glad to change and test it out. 

// Tips:
- Use a USB mouse at the catalina installer. Your trackpad will be very slow. It is solved in the post-installation.
- Boot the installation of macOS in Verbose mode. The loading bar will sometimes not move but in verbose you will see all progress. Do this by pressing the space bar in Clover on you macOS Installation and select Verbose. 
- If you don’t have another drive to boot (for example Windows) you can setup Clover Configurator so it doesn’t show the selection screen. For that go to Boot option in Clover Configurator and select “Fast”. 

# Pre-installation

// BIOS Settings:
1. Update your BIOS to the latest version
2. Open your BIOS settings with F10
3. Restore your BIOS defaults
4. Check the following settings:
* Boot settings - Custom Logo (Optional for Apple logo at boot)
* Boot settings - Disable fast boot
* Boot settings - Boot mode - UEFI hybrid (with CSM)
* Boot settings - Disable Secure boot (disabled if greyed out)
* Device configuration - Disable Wake on USB
* Built-in Device Options - Disable LAN/WLAN switching
* Built-in Device Options - Wake on LAN - Disable
* Port Options - Disable serial port
* Port Options - Disable 1394 port

// Making a USB installation:
1. Install Python and don’t forget to select “Add python to path” in the installer
2. Open GibMacOS (gibmacos.bat) as administrator
3. Select recovery mode with “R”
4. Select the option for Catalina with “full install” in the note
5. GibMacOS will create some folders, open them until you see a .pkg file
6. Copy the path of the PKG file
7. Insert your USB Stick at a usb port on your motherboard
- In this case it are the USB ports under your power button.
8. Open GibMacOS (makeinstall.bat) as administrator
9. Select your USB drive with the corresponding number
10. If the installer ask for your recovery path paste it here (pkg of step 6)
- This can take up to 15 minutes

// Preparing the USB drive:
1. Delete all files in the following folders on your USB drive
- /EFI/BOOT/BOOTX64.efi
- /EFI/CLOVER/drivers/BIOS
- /EFI/CLOVER/drivers/UEFI
- /EFI/CLOVER/kexts/Other
2. Delete the CLOVERX64.efi and config.plist in your /EFI/CLOVER folder
3. Open Clover pre-installation folder
4. Copy /EFI/CLOVER/ACPI to the /EFI/CLOVER/ folder on your USB drive
5. Copy all files from the following folders in the pre-installation folder to your USB drive
- /EFI/BOOT/
- /EFI/CLOVER/drivers/BIOS
- /EFI/CLOVER/drivers/UEFI
- /EFI/CLOVER/kexts/Other
6. And finally copy CLOVERX64.EFI, config.plist and drivers64UEFI to the clover folder on your USB drive.
7. Check the Clover folder. You now should have a copy of my Clover folder (a full copy won’t work, that’s why i use all the steps)

// Install MacOS Catalina:
1. Restart your laptop
2. Press F9 for your boot menu
3. Select Boot from EFI file
4. Navigate to /EFI/BOOT/BOOTX64.efi
5. Select this option and Clover will load
6. In clover, hit Enter on MacOS recovery installation
7. In the MacOS Installation open Disk Utility
8. Remove all volumes on the Internal SSD
9. Select Container Disk1 and select Erase
10. Name your disk (i like “Hackintosh HD”)
11. Select APFS as structure, and click erase. 
12. Close the disk utility and open the MacOS Installer
13. Follow the instructions in the installer
14. Your laptop will reboot and show Clover again select the installer from your internal SSD instead of the USB Drive.
- This can take up to 30 minutes
15. If your laptop reboots for the second time and shows Clover select Boot macOS from internal HDD.
- This can take up to 10 minutes

# Post-installation

// Clover Configurator:
1. Go to Finder > Settings
2. Enable your hard drive to show on your desktop
3. Unzip Clover Configurator
4. Move Clover Configurator to your Apps folder on your hard drive

// Setup your EFI disk:
1. Open Clover Configurator
- If you start Clover Configurator for the first time you need to go to Security in your settings panel and enable Clover to start. 
2. Click on Mount Efi and select Mount Partition. A Partition will show on your desktop
3. Rename the partitition to “HP_TOOLS” (for HP Custom boot logo)
4. Move the Hewlett-Packard folder to your EFI partition (for HP Custom boot logo)
5. Replace the EFI folder with the post-installation clover folder. 
* If you don’t want to use my bootloader theme you can delete the bootcamp_alpha folder from /EFI/CLOVER/themes/

// Make SMBios suitable for iCloud:
1. Open Clover Configurator
2. Select File > Open and open the config.plist you just moved to your EFI/CLOVER/
3. Click on SMBIOS
4. Select “Generate New” under both System - Serial Number as System - SmUUID

// Enable Audio:
1. Install VoodooHDA
2. Click next until you see the screen “Installationtype” Now select “Edit” on the left. 
3. Unfold the first option (VoodooHDA Clover UEFI/ESP and select macOS Catalina. 
4. Click Install. You will get voodoohda.kext in your clover folder and a extra menu in your preferences.
5. Go to your system preferences
6. Select VoodooHDA
7. On the left select Microphone (Both)
8. Slide the Monitor slider all the way down.  

// Disable hibernate (Your system will freeze at sleep otherwise):
1. Open up your terminal and run the following commands
2. sudo pmset -a hibernatemode 0
3. sudo rm /var/vm/sleepimage
4. sudo mkdir /var/vm/sleepimage

All Done! 
