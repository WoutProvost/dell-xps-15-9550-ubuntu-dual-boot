# dell-xps-15-9550-ubuntu-dual-boot
Follow these steps to dual boot an existing Windows 10 installation with Ubuntu on a Dell XPS 15 9550.

## Create a bootable Ubuntu USB stick
Download an `Ubuntu Desktop` version: https://ubuntu.com/download/desktop/. Download `Rufus`: https://rufus.ie/.
Use Rufus to create a bootable USB with the Ubuntu ISO.

## Disk partitioning
Open `Disk Management` in Windows and shrink the `C` drive with the desired space for Ubuntu. Leave that space unallocated.

## Disable fast startup
Disable `fast startup` in Windows so that Ubuntu can mount the drive when Windows is hibernated.

## Disable secure boot
Disable `secure boot` in the BIOS so that dual booting is allowed.

## ACHI
To make Ubuntu recognize your SSD, you need to switch your disk setting in the BIOS from `Raid On` to `ACHI`. Open a `Command Prompt` as Administrator in Windows and enter the following:
```Batch
bcdedit /set {current} safeboot minimal
```
Change the `SATA Operation Mode` to `AHCI` in the BIOS and reboot. Windows will now boot to safe mode. Open a `Command Prompt` as Administrator in Windows and enter the following:
```Batch
bcdedit /deletevalue {current} safeboot
```
Reboot again to exit safe mode.

## Install Ubuntu
Using the bootable USB, install Ubuntu. Select `Belgian` keyboard layout, `minimal` installation and install `alonside Windows`.

## Install NVIDIA graphics driver
Install the NVIDIA graphics driver in the `Software & Updates` program in the `Additional Drivers` tab. To switch graphics cards use one of the following commands:
```Bash
sudo prime-select intel
sudo prime-select nvidia
```
Note that switching graphics cards requires a full reboot. To see what graphics card is currently used, use the following command:
```Bash
nvidia-smi
```
If the GPU usage and other information are show, you're using the NVIDIA gpu, otherwise you're using the Intel gpu.

## Disable automatic updates
Set `Automatically check for updates` to `Never` in the `Updates` tab of the `Software & Updates` program, to prevent an error when trying to update via the terminal while the Ubuntu software updater is already checking automatically for updates.

## Clock synchronization
To synchronize the clock between Windows and Ubuntu, make Linux use local time with the following command:
```Bash
timedatectl set-local-rtc 1
```

# exFAT support
Enable support with the following command:
```Bash
sudo apt install exfat-fuse exfat-utils
```

## Improve battery life
Improve battery life with the following commands:
```Bash
sudo apt install tlp tlp-rdw
sudo tlp start
```
Show battery drain in real time with the following commands:
```Bash
sudo apt install powertop
sudo powertop
```

# Multi-Touch gestures
Add multi-touch gesture support for your trackpad with the following commands:
```Bash
sudo gpasswd -a $USER input
sudo apt install xdotool wmctrl libinput-tools
git clone https://github.com/bulletmark/libinput-gestures.git
cd libinput-gestures
sudo ./libinput-gestures-setup install
cd ..
rm -rf libinput-gestures
cp /etc/libinput-gestures.conf ~/.config/libinput-gestures.conf
libinput-gestures-setup autostart
libinput-gestures-setup start
```
You might need to relog for the changes to take effect. Put your personal gestures in the file `~/.config/libinput-gestures.conf`.






# Disable Bluetooth autostart on boot
...

# Lowest brightness setting on boot
...


TODO
https://support.system76.com/articles/graphics-switch-ubuntu/

## Night light slider
Andere repo best: https://extensions.gnome.org/extension/1276/night-light-slider/
Browser extension + ander ding
sudo apt install chrome-gnome-shell
Range van 1000 naar 6500
Tijd van actief 00:00 naar 00:00

# Change theme
See also other repo for theme, ...


TODO mention boot order wijzigen naar Ubuntu on top in BIOS
TODO aanpassen voor Ubuntu 20, Gnome Tweaks Settings + night light slider script ...
TODO libinput-gestures-setup restart voor als je het al gestart hebt
TODO restart tussen Windows en Linux lukt niet, enkel bij complete shutdown









# Application go back
gesture swipe right	3		xdotool key alt+Left

# Application go forward
gesture swipe left 3		xdotool key alt+Right

# Move to next workspace
gesture swipe left 4		xdotool key super+Page_Down

# Move to prev workspace
gesture swipe right 4		xdotool key super+Page_Up

# Show desktop
gesture swipe down 3		xdotool key super+d
gesture swipe down 4		xdotool key super+d

# Hide desktop
gesture swipe up 3			xdotool key super+d
gesture swipe up 4			xdotool key super+d