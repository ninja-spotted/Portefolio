---
title:  "Stock android replacements"
parent: Blog
permalink: "/blog/stock-android-replacements"
layout: default
date:   2026-09-22
last_modified_date: 2026-09-25
---

# Stock android replacements

Android phones (or smartphones I guess) have been with me for most my teenage years and young adult life. With the exception of my first phone (a dumb but quite capable Nokia phone), all devices I have had in my pants pocket have been Android and I have always enjoyed the experience of using it, even if nowadays it [feels less and less refreshing with every new update](https://www.androidpolice.com/android-updates-used-to-feel-revolutionary-now-they-feel-small-im-worried/).  

This lack of novelty, combined with more restrictive settings, pre-installed apps that you cannot fully uninstall or disable and more insights of how apps enforce almost no privacy concerns over my data made me want to investigate and find out what are the real alternatives to Android (or at least stock Android).

My old phone, the [Xiaomi Mi A2 Lite](https://en.wikipedia.org/wiki/Xiaomi_Mi_A2_Lite) is part of a Google program called [Android One](https://en.wikipedia.org/wiki/Android_One), a set of 3º party smartphones that would run a near-stock Android instead of the custom ROM and launchers that every phone manufacturer uses as well as a promised period of software updates. A version with the Xiaomi custom launcher also exists, and is called Xiaomi Redmi 6 Pro.

Now that the phone is way outside it's guarantee period and has served me well during nearly 6 years I have decided to take it for a spin again and try out some custom ROMs in it, since Xiaomi phones have easy to unlock bootloaders.


## The world of custom ROMs

One of the best resources online for custom android ROMs is [XDAForums](https://xdaforums.com/) where many communities are built around specific devices and can ask questions, get custom mods and even reviews.

In case of my phone, the [forum for it](https://xdaforums.com/c/xiaomi-mi-a2-lite.8005/) is still alive, with posts every now and then. For this phone model, we basically have the following options:

- [LineageOS](https://lineageos.org/): A free and open-source operating system for various devices, based on the Android mobile platform. The Xiaomi Mi A2 Lite is not officially supported by it, and does not show up in the official website, but many unofficial versions are available at [XDAForums like this one here](https://xdaforums.com/t/rom-android-15-unofficial-ota-lineageos-22-2-for-xiaomi-mi-a2-lite-daisy.4421213/).

- [Pixel Experience](https://get.pixelexperience.org/): An AOSP (Android Open Source Project) based ROM, with Google apps included and all Pixel goodies (launcher, wallpapers, icons, fonts, bootanimation). There are [official deprecated versions in their webpage](https://get.pixelexperience.org/sakura) but I haven't tested them.


## LineageOS installation

In this post, I will be going over LineageOS from the [forum post mentioned above](https://xdaforums.com/t/rom-android-15-unofficial-ota-lineageos-22-2-for-xiaomi-mi-a2-lite-daisy.4421213/). The guide and installation process can be found in [ItsVixano LineageOS Wiki](https://wiki.itsvixano.me/devices/daisy/) and contains everything to get the device up and running with LineageOS 22.2.


Other links that were useful:

- [Switching from stock ROM to custom ROMs](https://xdaforums.com/t/guide-installation-fix-switching-from-stock-rom-to-custom-roms-installing-stock-rom-after-a-brick-or-other-failures-mi-a2-lite-daisy.4351947/#post-85829819)
- [Unofficial TWRP recovery for Xiaomi Mi A2 Lite](https://xdaforums.com/t/recovery-3-5-2_9-2-mi-a2-lite-unofficial-twrp-recovery-for-xiaomi-mi-a2-lite.4178901/)

Since installation is pretty straighfoward, I will not detail the whole process. 

`fastboot boot '/home/user/Downloads/twrp-3.5.2_9-2-daisy-unofficial.img'`  
`adb push lineage-22.2-20250420-UNOFFICIAL-daisy.zip /sdcard`

After installation, go to Advanced -> Reboot to recovery and in LineageOS recovery do Factory reset -> Format data/factory reset -> Format data

### Installing Google apps

Apply update -> Apply from ADB and then
    
`adb sideload MindTheGapps-15.0.0-arm64-20250812_214357.zip`



## Android alternatives?

There are also brave souls who want their device to run other OSes not based on Android. That is the case of [PostmarketOS](https://postmarketos.org/), a Linux distribution for mobile devices which aims to extend the life of consumer electronics and giving people the control of their devices.

## PostmarketOS Installation

The following steps are based in their [official installation page for this phone](https://wiki.postmarketos.org/wiki/Xiaomi_Mi_A2_Lite_(xiaomi-daisy)) as well as other pages and resources. Start by cloning pmbootstrap, for building packages, creating installation images and flashing them to the phone:

    mkdir postmarket-os
    cd postmarket-os/
    git clone https://gitlab.postmarketos.org/postmarketOS/pmbootstrap.git
    cd pmbootstrap/

####  Plugging the Mi A2 Lite with android debugging mode turned on

    sudo fastboot oem unlock # Check if unlocked
    fastboot set_active b

####  Doing this will flash the "generic" postmarket port, which might not have the touchscreen drivers

    python pmbootstrap.py flasher flash_lk2nd
    python pmbootstrap.py flasher flash_rootfs

    python3 pmbootstrap.py zap
    python3 pmbootstrap.py init # choose Vendor: qcom Device codename: msm8953
    python3 pmbootstrap.py install

#### Since touchscreen was not working, need to edit touchscreen-compatible part and manually build lk2nd

    cd lk2nd/
    xed lk2nd/device/dts/msm8953/msm8953-xiaomi-daisy.dts

Edit the file to the following contents:

    // SPDX-License-Identifier: GPL-2.0-only

    /dts-v1/;

    #include <skeleton64.dtsi>
    #include <lk2nd.dtsi>

    / {
        qcom,msm-id = <QCOM_ID_MSM8953 0>;
        qcom,board-id = <QCOM_BOARD_ID(QRD, 1, 0) 9>;
    };

    &lk2nd {
        model = "Xiaomi Mi A2 Lite";
        compatible = "xiaomi,daisy";
        lk2nd,match-bootloader = "*DAISY*";

        lk2nd,dtb-files = "msm8953-xiaomi-daisy";

        panel {
            compatible = "xiaomi,daisy-panel", "lk2nd,panel";

            qcom,mdss_dsi_ili7807_fhdplus_video {
                compatible = "mdss,ili7807-fhdplus";
                touchscreen-compatible = "edt,edt-ft5406";
            };
            qcom,mdss_dsi_hx8399c_fhdplus_video {
                compatible = "himax,hx8399c-fhdplus";
                touchscreen-compatible = "edt,edt-ft5406";
            };
            qcom,mdss_dsi_otm1911_fhdplus_video {
                compatible = "mdss,otm1911-fhdplus";
                touchscreen-compatible = "edt,edt-ft5406";
            };
        };
    };

For building the lk2nd.img, I needed to install some depencencies. Then I could just use pmbootstrap to flash the OS into the phone:

    sudo apt install gcc-arm-none-eabi build-essential git
    sudo apt install device-tree-compiler
    make TOOLCHAIN_PREFIX=arm-none-eabi- lk2nd-msm8953
    fastboot flash boot_b build-lk2nd-msm8953/lk2nd.img
    fastboot set_active b
    fastboot reboot

    pmbootstrap flasher flash_rootfs

## Usage

TODO


### Conclusion

TODO
