# README

 ![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/53385f31-888a-4382-b733-c601e667a98d)

_____________________________________________________________________________________


# Table of Contents

- [0 What is this?](https://github.com/martinjrrr/README/blob/main/README.md#arch-linux-and-taking-care-of-your-install)
  - [0.1 Arch Linux and Taking Care of Your Install](https://github.com/martinjrrr/README/blob/main/README.md#arch-linux-and-taking-care-of-your-install)

- [1 Package Managers](#1-packages)
  - [1.1 Installing Packages Manually](#12-installing-packages-manually)

- [2 AMD's Display Issues](#2-amds-display-issues)
  - [2.1 Editing the EDID File](#21-editing-the-edid-file)
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

## What is this?


In the following `README.md` I'm going to explain how to setup KDE Arch and configure it so it just works, for this setup I'm choosing KDE Plasma as the DE because it is the best balance between extreme customizability and ease of use.

If anyone but myself uses this Repository for information I will reserve myself the right to not be held accountable for potentially bricking / breaking your systems or installs you have been warned!

_____________________________________________________________________________________

## Arch Linux and taking care of your install 


You should update your system at least once a week to prevent any issues from arising as the OS is bleeding edge and lives off of updating it regularly

Use either the `yay` or `sudo pacman -Syu` command to update your entire system and all packages except flatpaks

To update your flatpaks you'd need to put the command: `sudo flatpak update` into the terminal or update them from the software store you used to download them from, on KDE that store would most likely be 'Discover'

From time to time you can also clear the orphaned packages from your system by running `pacman -Qtdq | pacman -Rns` as the root user

_____________________________________________________________________________________

## 


















