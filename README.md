# About

_DatOS is built for people who would like to use their mobile phone as a general purpose internet router._

For many people, stable wired internet options are limited or unavailable - therefore cellular based internet options may be the only option. Unfortunately, there are some systemic barriers which generally cause problems for these types of users. The basic problems will be discussed below and also described how DatOS addresses these issues.

## Prevent Hotspot Limitations

The main issue DatOS addresses are the arbitrary usage-based restrictions that cellular carriers put on their unlimited data plans. 

Generally, carriers will detect, and limit/throttle hotspot, also known as "tethering", data usage; this essentially means your ability to share mobile data with other devices like your TV or computer. 

DatOS addresses this issue in 2 main ways:

- remove DUN/APN provisioning

- force TTL 64 for outgoing HTTP packets (no need to configure on each individual device)

In Progress:

- auto detect and reconnect when mobile data disconnected or throttled 

## Ease of Use

DatOS also seeks to make the phone to repurpose as a router, as such we make some basic changes for better user experience.

- default to 5GHZ wifi band

- default to use VPN for upstream (tethered) devices

- removes additional bloatware

- ships with F-droid, open source app store, for easy flexibility and customization options

In Progress:

- start/restart wifi tether on boot

## Compatible Devices

Currently, DatOS is supported on:

- LeEco Le S2 

> NOTE: If you would like to help expand DatOS support to new devices, please reach out to glenn@openinternet.cc

# Try It

## Preinstalled Device Kit

> Support DatOS development by purchasing a device kit with DatOS preinstalled from Open Internet Inc shop. 

![product](assets/prod.gif)

Package comes with: 

  - le eco s2 (preinstalled datos)
  - case
  - charging dock & cable
  - base station
  - warranty

<button name="button" style='font-weight: bold;color:#42b983;cursor:pointer;' onclick="https://openinternet.cc">Shop Now</button>

## Prebuilt Zip

Download latest official Prebuilt release to flash on your own device. 

Step 1) Download latest official prebuilt zip file   
Step 2) Skip to [installing](#installing) section

<button name="button" style='font-weight: bold;color:#42b983;cursor:pointer;' onclick="https://github.com/openinternet-cc/prebuilt">Download Now</button>

## Build it Yourself

> Click dropdown to see detailed instructions.

<details>

<summary style='font-weight:bold;font-size:large;'>Build Instructions</summary>

#### Requirements

- A LeEco Le 2 or compatible device  
- A relatively recent 64-bit computer (Linux, macOS, or Windows) with a reasonable amount of RAM and about 200 GB of free storage (more if you enable ccache or build for multiple devices). The less RAM you have, the longer the build will take. Aim for 16 GB RAM or more, enabling ZRAM can be helpful. Using SSDs results in considerably faster build times than traditional hard drives.  
- A decent internet connection and reliable electricity. :)  
- Some familiarity with basic Android operation and terminology.

#### Install Platform Tools

Install adb and fastboot, if you don't already have them installed.  
```
curl -L https://dl.google.com/android/repository/platform-tools-latest-linux.zip --output platform-tools-latest-linux.zip
unzip platform-tools-latest-linux.zip -d ~
```

Next, you'll need to add them to your path. Open `~/.profile` and add the following:
```~/.profile
# add Android SDK platform tools to path
if [ -d "$HOME/platform-tools" ] ; then
    PATH="$HOME/platform-tools:$PATH"
fi
``` 
Then, run `source ~/.profile` to update your environment.

#### Install Build Packages

To install the build packages, run the following:

```
apt-get update && \
apt-get install -y bc bison build-essential ccache curl flex g++-multilib gcc-multilib git gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5 libncurses5-dev libsdl1.2-dev libssl-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc zip zlib1g-dev
```

#### Create directories

You’ll need to set up some directories in your build environment.

To create them:  
```
mkdir -p ~/bin
mkdir -p ~/android/system
```
The ~/bin directory will contain the git-repo tool (commonly named “repo”) and the ~/android/system directory will contain the source code of DatOS.

#### Install the `repo` command:

Enter the following to download the repo binary and make it executable (runnable):  
```
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```

#### Configure git
Given that repo requires you to identify yourself to sync Android, run the following commands to configure your git identity:  
```
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

#### Turn on caching to speed up build

Make use of ccache if you want to speed up subsequent builds by running:
```
export USE_CCACHE=1
export CCACHE_EXEC=/usr/bin/ccache
```
and adding that line to your ~/.bashrc file. Then, specify the maximum amount of disk space you want ccache to use by typing this:  
```
ccache -M 50G
```

#### Initialize the DatOS source repository
```
cd ~/android/system
repo init -u https://github.com/openinternet-cc/android.git -b lineage-17.1
```

#### Download the source code

To start the download of the source code to your computer, type the following:
```
repo sync
```

#### Prepare the device-specific code

```
source build/envsetup.sh
breakfast s2
```

> NOTE: If you are building for a new or unsupported device, you will need to [do some extra steps here](https://wiki.lineageos.org/devices/s2/build#extract-proprietary-blobs) for your specific device.

#### Start the build

To start the build, type:
```
croot
brunch s2
```

Good job! If you made it this far, you have successfully built DatOS! Now, proceed to Install instructions.

</details>

<details>

<summary id='install' style='font-weight:bold;font-size:large;'>Installation Instructions</summary>


#### Requirements

- [TWRP S2 Recovery](https://dl.twrp.me/s2/)  
- `adb` & `fastboot` installed

#### Unlock the bootloader

1. Enable OEM unlock in the Developer options under device Settings, if present.  

2. Connect the device to your PC via USB.  
3. On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:   
```
adb reboot bootloader
```
4. Once the device is in fastboot mode, verify your PC finds it by typing:
```
fastboot devices
```
> TIP: If you see no permissions fastboot while on Linux or macOS, try running fastboot as root.

5. Now type the following command to unlock the bootloader: 
```
fastboot oem unlock-go
```

6. If the device doesn’t automatically reboot, reboot it. It should now be unlocked.  
7. Since the device resets completely, you will need to re-enable USB debugging to continue.  

#### Installing a custom recovery using fastboot

1. Download a custom recovery - you can download TWRP. Simply download the latest recovery file, named something like twrp-x.x.x-x-s2.img.  
2. Connect your device to your PC via USB.  
3. On the computer, open a command prompt (on Windows) or terminal (on Linux or macOS) window, and type:  
```
adb reboot bootloader
```
4. Once the device is in fastboot mode, verify your PC finds it by typing:  
```
fastboot devices
```
5. Flash recovery onto your device:  
```
fastboot flash recovery <recovery_filename>.img
```
> TIP: Some devices have buggy USB support while in bootloader mode, if you see fastboot hanging with no output when using commands such as fastboot getvar .. , fastboot boot ..., fastboot flash ... you may want to try a different USB port (preferably a USB Type-A 2.0 one) or a USB hub.

6. Now reboot into recovery to verify the installation:  
```
adb reboot recovery
```

#### Installing LineageOS from recovery

1. Download the DatOS Installation package zip from prebuilts repo  
2. If you are not in recovery, reboot into recovery.  
3. Now tap Wipe.  
4. Now tap Format Data and continue with the formatting process. This will remove encryption and delete all files stored in the internal storage.  
5. Return to the previous menu and tap Advanced Wipe, then select the Cache and System partitions and then Swipe to Wipe.  
6. Sideload the LineageOS .zip package:
  - On the device, select “Advanced”, “ADB Sideload”, then swipe to begin sideload.  
  - On the host machine, sideload the package using: adb sideload filename.zip.  
> TIP: If the process succeeds the output will stop at 47% and report adb: failed to read command: Success.

7. Once you have installed everything successfully, run `adb reboot`.

Congradulations! Youre done - Enjoy DatOS!

</details>

### Get assistance

If you have any issues, please get help on our community: 
- [Discord Server](https://discord.gg/2aMsFe6Ycz)

# Legal

## MIT License

Copyright 2021 Open Internet, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## Notice

By installing and using DatOS, you are agreeing to our [Terms of Service](https://terms.openinternet.cc).

