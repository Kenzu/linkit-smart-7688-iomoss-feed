# linkit-smart-7688-iomoss-feed
Feed for custom files add deps for the iomoss build

# Build the firmware from sources

This section describes how to build the firmware for LinkIt Smart 7688 and LinkIt Smart 7688 Duo from source codes with iomoss addons.


### Host environment
The following operations are performed under a Debian Stretch 9.5 environment. For a Windows or a Mac OS X host computer, you can install a VM for having the same environment:
* Download Debian Stretch 9.5 image from [http://www.debian.org](http://www.debian.org)
* Install this image with VirtualBox (http://virtualbox.org) on the host machine. 50GB disk space reserved for the VM is recommanded


### Steps
In the Debian system, open the *Terminal* application and type the following commands:

1. Install prerequisite packages for building the firmware:
    ```
    $ sudo apt-get install git g++ make libncurses5-dev subversion libssl-dev gawk libxml-parser-perl unzip wget python xz-utils
    ```

2. Download OpenWrt CC source codes:
    ```
    $ git clone https://git.openwrt.org/openwrt/openwrt.git/ -b openwrt-18.06
    ```
    
3. Prepare the default configuration file for feeds:
    ```
    $ cd openwrt
    $ cp feeds.conf.default feeds.conf
    ```
    
4. Add the LinkIt Smart 7688 iomoss feed:
    
    ```
    $ echo src-git linkit https://github.com/Kenzu/linkit-smart-7688-iomoss-feed.git >> feeds.conf
    ```
5. Update the feed information of all available packages for building the firmware:
    
    ```
    $ ./scripts/feeds update -a
    ```
6. Install all packages:
    
    ```
    $ ./scripts/feeds install -a
    ```
7. Prepare the kernel configuration to inform OpenWrt that we want to build an firmware for LinkIt Smart 7688:
    
    ```
    $ make menuconfig
    ```
    * Select the options as below:
        * Target System: `MediaTek Ralink MIPS`
        * Subtarget: `MT76x8 based boards`
        * Target Profile: `MediaTek LinkIt Smart 7688`
    * Save and exit (**use the deafult config file name without changing it**)
8. Start the compilation process:
    
    ```
    $ make V=99
    ```
9. After the build process completes, the resulted firmware file will be under `bin/targets/ramips/mt76x8/openwrt-ramips-mt76x8-LinkIt7688-squashfs-sysupgrade.bin`. Depending on the H/W resources of the host environment, the build process may **take more than 2 hours**.

10. You can use this file to do the firmware upgrade through the Web UI. Or rename it to `lks7688.img` for upgrading through a USB drive.

