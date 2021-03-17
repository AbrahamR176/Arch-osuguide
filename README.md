# Arch-osuguide

A more or less detailed explanation of installing osu on arch from zero, starting with the os..

**DISCLAIMER**

All the information that will be given here is based around my **OWN** experience. I am not responsible if anything breaks either in your linux installation or computer. 

Also this will be a guide for beginners. If you know your way around ThePoon's guide on installing osu!, then you probably do not need this guide.

If you have any questions, you can also just contact me if you have any question, if I have the time, I will help you out for sure.

**Credits to ThePoon for providing the guide I based mine on in: https://blog.thepoon.fr/osuLinuxAudioLatency/**

# Sections

- [Installing Linux](#Installing-Linux)
    - [Getting your system](#Getting-your-system)
    - [Flashing your USB](#Flashing-your-USB)
    - [installing system from USB](#installing-system-from-USB)
    - [Getting arch ready](#Getting-arch-ready)
        - [getting a custom kernel](#getting-a-custom-kernel)
        - [Getting your video driver](#Getting-your-video-driver)
        - [Setting up your CPU governor](#Setting-up-your-CPU-governor)
- [Installing osu!](#Installing-osu)
    - [Lutris and osu!](#Lutris-and-osu)
        - [Getting the patched wine.](#Getting-the-patched-wine)
    - [Setting up your audio.](#Setting-up-your-audio.)



# Installing Linux

## Getting your system
<!--Explain which file to download.-->
First of all, if you want to run osu! on arch, you need to have arch running in your computer.

All the information regarding the installation of arch can be found in https://wiki.archlinux.org/index.php/Installation_guide, but since you are not expected to understand everything right away, I would stick to something easier to use, like an installer of some distribution based on arch.

Some of these distrubutions are:

    * RebornOS (https://rebornos.org/)
    * EndevourOS (https://endeavouros.com/)
    * Manjaro (https://manjaro.org/)
    * ArcoLinux (https://arcolinux.com/)
    * Archlabs (https://archlabslinux.com/)

The flavor you choose is entirely up to you, but I personally use RebornOS and I've found great sucess using it.

## Flashing your USB
<!--Put pictures of flashing the system using Balena.-->

Once you find the flavor of arch you want to test, you have to get it installed, and for that, I recommend flashing the **.iso** of your OS in a USB stick.

**In the process of putting the OS into your USB, all the data inside of it will be wiped, make sure you make a proper backup in case you have anything important on it.**

To get the OS into your USB stick, I recommend using the tool called Balena Etcher. It works in both Windows and MacOS, and its free. https://www.balena.io/etcher/. 

Open Balena Etcher, select the .iso of your arch distro and USB stick, and then click on flash. it will take a while but eventually you will have your USB flashed and ready to use to install arch!.

## installing system from USB 
<!--This section is unfinished, make sure to detail the installation process better.-->

Make sure your flashed USB is plugged into your computer, then you have to restart into your boot menu, or BIOS to make sure you boot using your USB. This process is totally different from computer to computer, but the general idea is the same for most BIOS's out there.

Once you are in the Live enviroment, you can play with arch as much as you want, but understand that arch is not currently installed just yet. In the case that you are using RebornOS, there is a handy installer than will guide you through most of what you need.

<!--EXPLAIN HOW TO PARTITION-->

## Getting arch ready

Once you have arch installed, you can probably just boot into it using Grub or by changing the boot order in your BIOS.

First you have to know the following terms, which are going to be used throughout this guide:

Command | Definition
------------ | -------------
Install/Download| pacman -S **appname**
nano/edit | nano **nameoffile**

**to save the changes and exit nano, press CONTROL + O, enter, and then CONTROL + X.**

Also you will be asked to use the terminal a lot, make sure you know which terminal you have installed in your system, and also some basic commands.

Command | Definition
------------ | -------------
ls | Shows every file in the folder your terminal is currently is.
cd | moves your terminal to the folder specified: `cd Downloads`, ``cd ..`` moves you back.


### getting a custom kernel

There are multiple kernels in osu, you can pick whichever one you want, but I recommend using Linux-zen, since it is what ThePoon recommends and has worked most of the time for me.

    pacman -S linux-zen linux-zen-headers

Once it is installed, you will have to update your grub for it to show it so you can access it. 

    grub-mkconfig -o /boot/grub/grub.cfg

Once that finishes, you can restart and the linux-zen option will appear on the list to pick, when your computer boots you will be running Linux-zen!.

**If you use an nvidia gpu, make sure you install the nvidia-dkms driver, or else your computer wont boot on linux-zen.**

    pacman -S nvidia-dkms

You can always read the wiki for more information.

### Getting your video driver

Not all linux distributions come with the appropiate driver preinstalled. If you have an nvidia GPU you are most likely using Nouveau, which is NOT good for gaming and wouldn't advice using it.

To check which driver you are running:

    lspci -nnk

    01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GP104 [GeForce GTX 1060 6GB] [10de:1b83] (rev a1)
	Subsystem: Gigabyte Technology Co., Ltd Device [1458:371a]
	Kernel driver in use: nvidia

Mine is currently the `nvidia` driver, but in case it is not, you can install it easily by doing

**For nvidia**

    pacman -S nvidia lib32-nvidia-utils

**For AMD**

    pacman -S amdgpu

I don't personally own an AMD GPU, so I can't tell which driver is better, but the wiki might help you out better. https://wiki.archlinux.org/index.php/AMDGPU

### Setting up your CPU governor

The CPU governor can have HUGE impact in performance, and not all cpus come with performance in mind. you can just change your governor to something that fits your needs better.

    pacman -S cpupower

then to put the performance governor:

    cpupower frequency-set -g performance

This will give you better performance not only in osu, but in your linux system overall.

# Installing osu

Now the fun starts, we are going to be installing osu! using lutris, which makes the entire process easier.

## Lutris and osu

First of all, get lutris:

    pacman -S lutris

For osu to work you also need wine to be installed:

    pacman -S wine lib32-gnutls lib32-libxcomposite

`lib32-libxcomposite` and `lib32-gnutls` are installed to get rid of some problems that might show up down the line, they are optional and osu! might work without it.

Once you have lutris installed, open it and search up for osu! in the browser, once you find it, install the `Windows` version and press continue as many times as it asks you to.

If everything went right then your osu will be up and running, but once you start to play you will notice that the audio is not as good as it could be, it could be stuttery or straight up broken, lets fix that.

### Getting the patched wine

Normally you would have to download wine and compile the patches by yourself, I recommend downloading a precompiled wine since it works just fine.

get it at https://5124.mywire.org/HDD/Downloads/wine-osu-4.13-1-x86_64.pkg.tar.xz, **credits to ThePoon and the community in his discord for providing this wine compilation.**

Then you have to extract it, if you saved the file in downloads, then you can do:

    tar -xvf wine-osu-4.13-1-x86_64.pkg.tar.xz

Now go to lutris, right click osu and configure, then go to `Runner options`, and for `Wine version`, select custom and tick the `Advanced options` box in the bottom of the settings.

Now you have to browser to where your `wine` file in the folder you downloaded is, in my case it is. It should look like: 

    .../wine-osu/bin/wine


## Setting up your audio

This is by far the hardest part, but don't be scared, its not that hard.

Change your audio priority, copy and paste the entire thing.

    echo "USER - nice -20
    USER - rtprio 99" >> /etc/security/limits.conf

copy and paste the entire command, and replace USER with your username, you can find your username in your terminal.

Create a new folder in /etc/pulse/ called pulse/daemon.conf.d: 

    mkdir -p /etc/pulse/daemon.conf.d/

Create the file containing the following settings, copy and paste the entire thing:

    echo "high-priority = yes
    nice-level = -15

    realtime-scheduling = yes
    realtime-priority = 50

    resample-method = speex-float-0

    default-fragments = 2 # Minimum is 2
    default-fragment-size-msec = 2 # You can set this to 1, but that will break OBS audio capture." | sudo tee -a /etc/pulse/daemon.conf.d/10-better-latency.conf

Now edit `/etc/pulse/daemon.conf.d/10-better-latency.conf` and change both the `default-fragments` and `default-fragment-size-msec`, this is where some trial and error comes into place, if your audio sounds broken or cracking, increase both of these numbers, in my case I use default-fragments = 6 and default-fragment-size-msec = 3.

    sudo nano /etc/pulse/daemon.conf.d/10-better-latency.conf

Now lets edit the pulseaudio settings file and add the following line:

    sudo nano /etc/pulse/default.pa

Using the arrow keys scroll down till you see something like this:

    ### Automatically load driver modules depending on the hardware available
    .ifexists module-udev-detect.so
    load-module module-udev-detect 
    .else

Add ``tsched=0`` to the end of ``load-module module-udev-detect ``

    ### Automatically load driver modules depending on the hardware available
    .ifexists module-udev-detect.so
    load-module module-udev-detect tsched=0
    .else

that should be all for your audio, make sure you restart pulseaudio for it to take effect.

    pulseaudio -k

Now lets set up some settings in your lutris.

Open lutris and right click on osu!, and then press configure. In the `System options`, scroll down to environment variables and add the following two values:

Key | Value
------------ | -------------
STAGING_AUDIO_DURATION | **VALUE**
STAGING_AUDIO_PERIOD | **VALUE**

I recommend starting with values of `10000`, and if the game audio is still broken after that, keep increasing both until it doesnt.

and if everything is properly configured, your osu! should start and the audio shouldn't be an a mess!.





