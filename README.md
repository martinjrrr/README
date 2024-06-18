# README

 ![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/53385f31-888a-4382-b733-c601e667a98d)

_____________________________________________________________________________________


# Table of Contents

- [0 What is this?](https://github.com/martinjrrr/README/blob/main/README.md#arch-linux-and-taking-care-of-your-install)
  - [0.1 Arch Linux and Taking Care of Your Install](https://github.com/martinjrrr/README/blob/main/README.md#arch-linux-and-taking-care-of-your-install)

- [1 Package Managers](https://github.com/martinjrrr/README/blob/main/README.md#package-managers)
  - [1.1 Installing AUR Packages Manually](https://github.com/martinjrrr/README/blob/main/README.md#installing-aur-packages-manually)

- [2 AMD's Display Issues](https://github.com/martinjrrr/README/blob/main/README.md#amds-display-issues)
  - [2.1 Editing the EDID File](https://github.com/martinjrrr/README/blob/main/README.md#editing-the-edid-file)
  - [2.2 Adding the Kernel Parameter](https://github.com/martinjrrr/README/blob/main/README.md#adding-the-kernel-parameter)
  - [2.3 Applying the Kernel Parameter](https://github.com/martinjrrr/README/blob/main/README.md#applying-the-kernel-parameter)

- [3 Basic Linux Commands](https://github.com/martinjrrr/README/blob/main/README.md#basic-but-important-linux-commands)
  - [3.1 ls - List Command](https://github.com/martinjrrr/README/blob/main/README.md#ls---list-command)
  - [3.2 more ls commands](https://github.com/martinjrrr/README/blob/main/README.md#more-ls-commands-and-their-flags)
  - [3.3 mkdir - Make Directory Command](https://github.com/martinjrrr/README/blob/main/README.md#makedir-command)
  - [3.4 mv - move and rename]()

- [4 Aesthetics](https://github.com/martinjrrr/README/blob/main/README.md#aesthetics)
  - [4.1 Making Your Browser Startpage Aesthetic](https://github.com/martinjrrr/README/blob/main/README.md#aesthetic-firefox-startpage)
  - [4.2 Making Your Bash Terminal Look Good](https://github.com/martinjrrr/README/blob/main/README.md#making-your-bash-terminal-look-aesthetic)
  - [4.3 Making Your Bootloader Look Good](https://github.com/martinjrrr/README/blob/main/README.md#making-your-bootloader-look-good)


- [5 Grub Bootloader](https://github.com/martinjrrr/README/blob/main/README.md#grub-bootloader)
  - [5.1 activating os-prober and update-grub script](https://github.com/martinjrrr/README/blob/main/README.md#activating-os-prober-and-update-grub-script)
 

- [6 Extras](https://github.com/martinjrrr/README/blob/main/README.md#extras)
  - [6.1 Spotify Daemon and Spotify in your terminal](https://github.com/martinjrrr/README/blob/main/README.md#spotify-daemon-and-spotify-in-your-terminal)
  - [6.2 Radeon Fan Control](https://github.com/martinjrrr/README/blob/main/README.md#radeon-fan-control)
  - [6.3 OPENRGB RGB Software](https://github.com/martinjrrr/README/blob/main/README.md#openrgb-rgb-software)
  - [6.4 Firefox about:config Tweaks](https://github.com/martinjrrr/README/blob/main/README.md#firefox-aboutconfig-tweaks)
  - [6.5 Fix Minecraft not Connecting to the Sound engine](https://github.com/martinjrrr/README/blob/main/README.md#fix-minecraft-not-connecting-to-the-sound-engine)
  - [6.6 Nice to have programs](https://github.com/martinjrrr/README/blob/main/README.md#nice-to-have-programs)
  - [6.7 UBLOCK Youtube Shorts Block List](https://github.com/martinjrrr/README/blob/main/README.md#ublock-origin-youtube-shorts-blocklist)
 
 
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

## Installing AUR packages Manually

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

_____________________________________________________________________________________

# Basic but Important Linux Commands

## ls - List Command

[Guide by Redhat on basic navigation](https://www.redhat.com/sysadmin/navigating-linux-filesystem)

[More specific guide for using ls](https://www.howtogeek.com/448446/how-to-use-the-ls-command-on-linux/)

[Guide on how to use the tree command with examples](https://linuxhandbook.com/tree-command/)

`cd /home/user/Documents/` to navigate into the Documents folder located in the users home directory

`cd ~` to navigate back to your home directory


| ls -flag | what they are for |
| --- | --- |
| `ls` | to list the current directories contents |
| `ls -<nr of rows>` | to change the number of rows shown when listing the directory |
| `ls <directory name>` | to list a certain directory |
| `ls <characters>*` | to list any files with the selected string of characters | 
| `ls <character>?` | to list any files with the selected single character |
| `ls *.png` | to list any files with the selected file format, in this case the .png format |
| `ls --hide=*.png` | to hide all files with the given file extension |
| `ls -l` | is the so called: "long listing" option which gives you more details on each file |

The long listing lists a lot of information at once, in this case it is the file type, the user, the group, the file size, date the file was last edited, with month, date, exact time to the minute and year listed respectfully.
There are different types of files, depending on the first character it could mean:

The very first character represents the file type:

    -: A regular file.
    b: A block special file.
    c: A character special file.
    d: A directory.
    l: A symbolic link.
    n: A network file.
    p: A named pipe.
    s: A socket.

### More LS Commands and their flags:

| ls - flag | what they are for |
| --- | --- |
| `ls -l -h` | using the -h flag ls displays the filesize in human-readable sizes, converting kilobites to mb |
| `ls -l -a` | using the -a flag all files including hidden files will be shown |
| `ls -l -A` | using the -a flag almost all files will be shown, omitting . and .. entries from your list, resulting in an overall more legible window |
| `ls -l -R` | using the -R (recursive) flag lists all files in each subdirectory |
| `ls -n` | using the -n flag lists the user ID instead of the user name |
| `ls -X -1` | using the -X -1 flags lists the files by extension type in alphabetical order, directories will be listed first |
| `ls -l -h -S` | using the flags -l (list) -h (human-readable) and the -S flag will sort the files by size. |
|`ls -l -t` | using the flag -t will sort files by when they were last modified |
| `ls -l -h -S -r` | using the -r flag will reverse any sort orders |
 
use `ls -t | head -1` to get the newest file in the directory

use `ls -t | tail -1` to get the oldest file in the directory 

## makedir command

How to use the `make` directory command

`mkdir [OPTION] [DIRECTORY]` this is the commands syntax

`mkdir /home/user/Documents/exampledir` to make a new directory called 'exampledir' in the Documents folder of our Linux system




an example of a file tree and the command that creates it:

`makedir -p /home/user/Documents/folder1,folder2/subfolder1,subfolder2/`

     Documents/
     ├──folder1
     |   ├──subfolder1
     |   └──subfolder2
     |
     └──folder2
         ├──subfolder1
         └──subfolder2
         




an example of a more complicated file tree and the command that creates it:

`mkdir -p Music/{Jazz/Blues,Folk,Disco,Rock/{Gothic,Punk,Progressive},Classical/Baroque/Early}`

    Music/
    ├──Classical
    |   └──Baroque
    |       └──Early
    ├──Disco
    ├──Folk
    ├──Jazz
    |   └──Blues
    └──Rock
        ├──Gothic
        ├──Progressive
        └──Punk

   



`sudo makedir` to make a directory in a folder that needs super user permissions

`sudo chown -R user /home/user/Documents/exampledir/*` is what we'll use if we want to take ownership of the folder exampledir and all sub files and folders

`sudo chown -R user:user /home/user` if any of the user directories are owned by root

_____________________________________________________________________________________

# Aesthetics

In this chapter we'll take a look at making your system nicer to look at and less of a strain on the eyes

## Aesthetic Firefox startpage

[HTML Startpage Generator](https://github.com/PrettyCoffee/yet-another-generic-startpage)

![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/809d81d8-42d9-46ff-b83d-316d9e135d3c)

You could also use the shown config, Download the *firestart.zip* and select the HTML file as your Firefox homepage
If you want to modify my given example navigate to the Startpage generator and feed the *ls-backup.json* into the site

## Making your Bash Terminal look aesthetic

We are now going to Setup an equivalent to OhMyZSH to make our terminal look better

    git clone https://github.com/christitustech/mybash

    cd mybash

    ./setup.sh

We'll download the Jetbrains Mono Nerdfont to our system so that we can set it in the terminal:

    cd ~/Downloads &&
    curl -L -o JetBrainsMono.zip "https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/JetBrainsMono.zip"

![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/03247de1-ff2f-49fe-8947-ad50fa507f81)

## Making Your Bootloader Look Good

Now we will theme the Bootloader and make it presentable 

    $ git clone https://github.com/ChrisTitusTech/Top-5-Bootloader-Themes

    $ cd Top-5-Bootloader-Themes

      sudo ./install.sh

choose the theme that you like most and apply

_____________________________________________________________________________________


# Grub Bootloader

The Grub bootloader is likely used if you are dual booting your system, you can add and remove entries, we'll go over how to add an entry thats missing in the next steps.

## activating os-prober and update-grub script

Open the grub config in your Text editor of choice: 

`kate /etc/default/grub`
uncomment "GRUB_DISABLE_OS_PROBER=false" and save the file

Create a file in the path "/usr/sbin/" this will be a shell script to update grub with

`cd /usr/sbin/`

`touch update-grub`

open the file with your text editor of choice:

`kate update-grub`

paste the following text and save the file
    
    #!/bin/sh
    set -e
    exec grub-mkconfig -o /boot/grub/grub.cfg "$@"

afterwards execute these two commands: 

    sudo chown root:root /usr/sbin/update-grub &&
    sudo chmod 755 /usr/sbin/update-grub

Now you should be able to run the command `update-grub` to update your grub config

If we now want to add Windows to our Grub bootloader for example, we would run: 
    
    sudo os-prober &&
    update-grub

_____________________________________________________________________________________

# Extras

In the following we'll take a look at optional, nice to have but not necessary packages and how to install them

## Spotify Daemon and Spotify in your terminal

Follow the instructions below starting with installing the necessary packages using yay

`spotify-tui`

When spotify-tui is installed you will need to run it by writing `spt` into your terminal of choice

spt will then ask you for your spotify `Client ID`and `Client Secret` which you'll have to get from the spotify developer dashboard for which there are many guides on how to setup an application and get your ID + Secret respectively

**Once you've entered both the Client ID and Client secret all should be working and you'll see a User Interface pop up**

now to use the UI which we've installed we'll need a daemon to stream Spotify to, for that we'll use the spotifyd-daemon

`spotifyd` is the package name, download it using yay or refer to the projects github to get more information

now copy the spotifyd.conf from my github repo enter your username and password into the file and make a folder for the config to be in

`mkdir /home/user/.config/spotifyd`

Then copy the file from downloads to the new directory

`cd ~/Downloads/`

`cp spotify.conf /home/user/.config/spotifyd`

Now type the following lines into the terminal you want to use for the UI to live in:

`spotifyd`

`spt`

If the daemon gives you any issues like playing two streams at once type the following into the terminal to restart the daemon

`killall spotifyd`

`spotifyd`

![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/f5a55a60-db9d-4672-a057-19e71f9e24ff)

In addition to spotifyd and spotify-tui you can install cava
a visualizer, copy my config into ~/.config/cava/ to apply the design shown in the screenshot above


## Radeon Fan Control

All of these are to be installed using the yay package manager or the guide on installing AUR packages above

`mesa-git` FOSS GPU Drivers

`radeon-profile-git` Radeon Overclocking and Fan Control utility

`radeon-profile-daemon-git` The needed daemon to run the Previous software

After finishing the Download you'll need to run the following commands in the terminal

    systemctl enable radeon-profile-daemon.service &&
    systemctl start radeon-profile-daemon.service

![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/f0a78723-c402-460a-b140-86470acc19e4)


**Now Radeon-profile should be working and showing modules like fan control**


## OPENRGB RGB Software

OpenRGB is an open source utility to control all your RGB using one software solution

`openrgb` / `openrgb-git`

`i2c-tools`

Before launching we'll need to execute a few commands

     $ sudo modprobe i2c-dev

     $ sudo groupadd --system i2c

     $ sudo usermod $USER -aG i2c
 
       sudo touch /etc/modules-load.d/i2c.conf &&

       sudo sh -c 'echo "i2c-dev" >> /etc/modules-load.d/i2c.conf'

![image](https://github.com/martinjrrr/Linux.dots/assets/91160845/211dd1fd-05cb-4ef1-a02e-c1a611ae3856)

**Now OpenRGB should also show RAM Modules**


## Firefox about:config Tweaks

head to about:config in your address bar for all of these

Disable fullscreen popup when fullscreening a video:
    
    full-screen-api.warning.timeout -> set to 0

Disable translate option:
       
    browser.translations.automaticallyPopup 
    browser.translations.enable
    browser.translations.panelShown

## FIX Minecraft not connecting to the sound engine

You'll need to add the line `drivers-alsa` to `/etc/openal/alsoft.conf`

`sudo mkdir /etc/openal/`  if the directory does not exist

`alsoft.conf` if the file does not exist to create it in your ~/Downloads/ directory

add the line `drivers-alsa` and save the file

`cd ~/Downloads/`

`sudo cp alsoft.conf /etc/openal/`

**Start / Restart Minecraft and it should have a working sound engine**


## Nice to have Programs

`kate` -> Text Editor

`vscodium` -> Opensource VSCode binaries

`thunderbird` -> Mozillas Mail Client

`kgamma5` -> X11 Gamma control for KDE Systems

`ani-cli` -> Watch and download anime from your terminal

`mangal` -> Read and download manga from your terminal

`speedtest-cli` -> cli to test your connection speeds from your terminal 

`Discover` + `packagekit-qt5` -> KDE's own software store

`Obsidian` -> Notetaking app with community integration

`clam AV` -> Antivirus software


## UBLOCK Origin Youtube Shorts Blocklist

Add the following text via. copy and paste to your uBlock Origin filter list to get rid of pesky Youtube Shorts

    ! Title: Hide YouTube Shorts
    ! Description: Hide all traces of YouTube shorts videos on YouTube
    ! Version: 1.8.0
    ! Last modified: 2023-01-08 20:02
    ! Expires: 2 weeks (update frequency)
    ! Homepage: https://github.com/gijsdev/ublock-hide-yt-shorts
    ! License: https://github.com/gijsdev/ublock-hide-yt-shorts/blob/master/LICENSE.md

    ! Hide all videos containing the phrase "#shorts"
    youtube.com##ytd-grid-video-renderer:has(#video-title:has-text(#shorts))
    youtube.com##ytd-grid-video-renderer:has(#video-title:has-text(#Shorts))
    youtube.com##ytd-grid-video-renderer:has(#video-title:has-text(#short))
    youtube.com##ytd-grid-video-renderer:has(#video-title:has-text(#Short))

    ! Hide all videos with the shorts indicator on the thumbnail
    youtube.com##ytd-grid-video-renderer:has([overlay-style="SHORTS"])
    youtube.com##ytd-rich-item-renderer:has([overlay-style="SHORTS"])
    youtube.com##ytd-video-renderer:has([overlay-style="SHORTS"])
    youtube.com##ytd-item-section-renderer.ytd-section-list-renderer[page-subtype="subscriptions"]:has(ytd-video-renderer:has([overlay-style="SHORTS"]))

    ! Hide shorts button in sidebar
    youtube.com##ytd-guide-entry-renderer:has-text(Shorts)
    youtube.com##ytd-mini-guide-entry-renderer:has-text(Shorts)
 
    ! Hide shorts section on homepage
    youtube.com##ytd-rich-section-renderer:has(#rich-shelf-header:has-text(Shorts))
    youtube.com##ytd-reel-shelf-renderer:has(.ytd-reel-shelf-renderer:has-text(Shorts))

    ! Hide shorts tab on channel pages
    ! Old style
    youtube.com##tp-yt-paper-tab:has(.tp-yt-paper-tab:has-text(Shorts))
    ! New style (2023-10)
    youtube.com##yt-tab-shape:has-text(/^Shorts$/)

    ! Hide shorts in video descriptions
    youtube.com##ytd-reel-shelf-renderer.ytd-structured-description-content-renderer:has-text("Shorts remixing this video")

    ! Remove empty spaces in grid
    youtube.com##ytd-rich-grid-row,#contents.ytd-rich-grid-row:style(display: contents !important)




