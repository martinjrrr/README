# README

 ![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/53385f31-888a-4382-b733-c601e667a98d)

_____________________________________________________________________________________


# Table of Contents

- [0 What is this?](https://github.com/martinjrrr/README/blob/main/README.md#arch-linux-and-taking-care-of-your-install)
  - [0.1 Arch Linux and Taking Care of Your Install](https://github.com/martinjrrr/README/blob/main/README.md#arch-linux-and-taking-care-of-your-install)

- [1 Package Managers](https://github.com/martinjrrr/README/blob/main/README.md#package-managers)
  - [1.1 Installing Packages Manually](https://github.com/martinjrrr/README/blob/main/README.md#installing-packages-manually)

- [2 AMD's Display Issues](https://github.com/martinjrrr/README/blob/main/README.md#amds-display-issues)
  - [2.1 Editing the EDID File](https://github.com/martinjrrr/README/blob/main/README.md#editing-the-edid-file)
  - [2.2 Adding the Kernel Parameter](#22-adding-the-kernel-parameter)
  - [2.3 Applying the Kernel Parameter](#23-applying-the-kernel-parameter)

- [3 Basic Linux Commands](#3-basic-linux-commands)
  - [3.1 ls - List Command](#31-ls---list-command)
  - [3.2 mkdir - Make Directory Command](#32-mkdir---make-directory-command)

- [4 Aesthetics](#4-aesthetics)
  - [4.1 Making Your Browser Startpage Aesthetic](#41-making-your-browser-startpage-aesthetic)
  - [4.2 Making Your Bash Terminal Look Good](#42-making-your-bash-terminal-look-good)
  - [4.3 Making Your Bootloader Look Good](#43-making-your-bootloader-look-good)


- [5 Grub Bootloader](5-grub)  
  - [5.1 activating os-prober and update-grub script](51-osgrub)
 

- [6 Extras](6-extras)
  - [6.1 Spotify Daemon and Spotify in your terminal](61-spotify-daemon-and-terminal-app)
  - [6.2 CAVA Visualizer and Config pasting](62-cava)
  - [6.3 Radeon Fan Control](63-radeonfancontrol)
  - [6.4 OPENRGB RGB Software](64-openrgb)
  - [6.5 Firefox about:config Tweaks](65-about)
  - [6.6 UBLOCK Youtube Shorts Block List](66-ublock)
 
_____________________________________________________________________________________

# What is this?


In the following `README.md` I'm going to explain how to setup KDE Arch and configure it so it just works, for this setup I'm choosing KDE Plasma as the DE because it is the best balance between extreme customizability and ease of use.

If anyone but myself uses this Repository for information I will reserve myself the right to not be held accountable for potentially bricking / breaking your systems or installs you have been warned!


## Arch Linux and taking care of your install 


You should update your system at least once a week to prevent any issues from arising as the OS is bleeding edge and lives off of updating it regularly

Use either the `yay` or `sudo pacman -Syu` command to update your entire system and all packages except flatpaks

To update your flatpaks you'd need to put the command: `sudo flatpak update` into the terminal or update them from the software store you used to download them from, on KDE that store would most likely be 'Discover'

From time to time you can also clear the orphaned packages from your system by running `pacman -Qtdq | pacman -Rns` as the root user

_____________________________________________________________________________________

# Package Managers

We'll be using Yay as an AUR Helper and Pacman as our package manager

## Installing packages Manually

To install an AUR package without a package manager you first grab the AUR url of the package you want to install, in this example we'll be taking the brave-nightly package

`git clone https://aur.archlinux.org/brave-nightly-bin.git`

`cd brave-nightly-bin`

`kate PKGBUILD`

After reading and verifying that the packages are secure enter:

`makepkg` or to finish the install right away enter `makepkg -sri`

`ls`

sudo pacman -U brave-nightly-bin-xx.x.x-x-x86_64.pkg.tar.zst

agree to the prompt asking to install with `Y`

to build packages faster open `/etc/makepkg.conf` 
and edit the line which says `#MAKEFLAGS="-j4"`
enter the amount of threads you want to use for building packages instead of 4
to improve the build time.

_____________________________________________________________________________________

# AMD's Display Issues

One of the main issues I've encountered on my system is that my HDMI Monitor does not use RGB 0-255, this makes the greys washed out and consuming content on the system unbearable to me, luckily there is a fix by editing the monitors EDID

## Editing the EDID file 
To follow this guide you can either download the `modified_edid.bin` and save it to `~/Downloads/` which may only work for my monitor or follow the step by step guide on how to edit your own EDID file

Open a terminal:

`find /sys/devices/pci*/ -name edid` to find the EDID used by your monitor 

Output should look something like this:

`/sys/devices/pci0000:00/0000:00:03.1/0000:2b:00.0/0000:2c:00.0/0000:2d:00.0/drm/card1/card1-DP-1/edid`

You'll need to choose the connector of your monitor, for me it is card1-DP-1

Next I'll cd into the directory where my EDID is located and copy it:

`cd /sys/devices/pci0000:00/0000:00:03.1/0000:2b:00.0/0000:2c:00.0/0000:2d:00.0/drm/card1/card1-DP-1`

`cp edid ~/Downloads/`

Next you'll need to download wxEDID:

flatpak install https://dl.tingping.se/flatpak/wxedid.flatpakref

open the edid file which is now located in the `~/Downloads/` directory using wxEDID

edit it to disable YCbCr support:


    SPF: Supported features -> change value of vsig_format to 0b00
 
    CHD: CEA-861 header -> change the value of YCbCr420 and YCbCr444 to 0
 
    VSD: Vendor Specific Data Block -> change the value of DC_Y444 to 0
 

Afterwards save the EDID binary and rename it to "modified_edid.bin" and save it to ~/Downloads/

## Adding the Kernel Parameter

Open a Terminal: 

    $ cd ~/Downloads/

    $ sudo cp modified_edid.bin /usr/lib/firmware/edid/

    $ sudo mkdir /usr/lib/firmware/edid/ if the directory does not exist

open the file /etc/default/grub with your preferred text editor and copy:

`drm.edid_firmware=edid/modified_edid.bin` after `GRUB_CMDLINE_LINUX_DEFAULT=` and `GRUB_CMDLINE_LINUX=` then save

## Applying the Kernel Parameter

Enter the following into your terminal

`sudo grub-mkconfig -o /boot/grub/grub.cfg` in the terminal to apply the kernel patch

**After a reboot the monitor should switch to the correct RGB values upon login**



