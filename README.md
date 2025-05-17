# KMONAD setup for Linux and Windows

This repo is for my personal use, but if you happen to come across it feel free to grab it and use it for yourself. 

This is based off of the wonderful **KMONAD** project https://github.com/kmonad/kmonad/ which allows for low level mapping of keyboards without requiring QMK capapilities. 

## What It Does 
The config as in this repo will allow for: 
* **CAPSLOCK** to be remapped to **ESC** when tapped
* **CAPSLOCK** to effect keys **h, j, k, l** to be **left, down, up and right** respectively - allowing for cursor movement that mimics vim movements even when in insert mode without having to move the hand to the arrow keys 
* **CAPSLOCK** to effect keys **left and right** so that they will effectively be home and end keys, mimicing the functionality of holding Fn on thinkpad with arrow keys

## The Config Files
There are two config files: 
* **mythinkpad_kbd** (tested and currently being used on a ubuntu distro)
* **mythinkpad_windows_kbd** (to be tested on on windows)

The reason I had two different files is that I run a dual boot on my computer and require windows for some work purposes. As you can imagine, the file with the windows suffix is for usage on windows

## Usage
To test the config: run the relevant executable for the sysmtem being worked on using the relevant config file as the first argument

For example:
```
./kmonad mythinkpad.kbd
```
For a first time user, it might be surprising that this will be a blocking operation and take over the terminal. If you need to exit, in most terminals you will be able to do so using a **SIGINT** command which can be sent using **CTRL + C**

Do note however that the keykindings effected by keymonad will only be in effect while the program is actually running during testing - so you would probably just want to fire up notepad or some kind or editor to test the functionality while you have this program active in a terminal.

If there are no errors, and all is good, then we can move to configuring your system so that starting of the program is automatic.

## Kmonad on Startup - Linux
* copy the linux kmonad binary into the local system binary folder
```
sudo cp ./kmonad /usr/bin/kmonad
```
the file **kmonad.service** needs to be stored at **/etc/systemd/system/kmonad.service**. Note that for your usage, there will probably be a requirement to repoint the argument in the file to where you're storing you configuration file.


With the service file saved in the relevant location, start the service
```

sudo systemctl start kmonad.service
sudo systemctl enable kmonad.service
```

Your configuration should now be avaialable to you at startup, without having to manually start the program. Restart and test.