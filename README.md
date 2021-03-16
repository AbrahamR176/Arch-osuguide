# Arch-osuguide

A more or less detailed explanation of installing osu on arch from zero, starting with the os..

**DISCLAIMER**

All the information that will be given here is based around my **OWN** experience. I am not responsible if anything breaks either in your linux installation or computer. 

Also this will be a guide for beginners. If you know your way around ThePoon's guide on installing osu!, then you probably do not need this guide.

If you have any questions, you can also just contact me if you have any question, if I have the time, I will help you out for sure.

## Installing-Linux

### Getting your system
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

### Flashing your USB
<!--Put pictures of flashing the system using Balena.-->

Once you find the flavor of arch you want to test, you have to get it installed, and for that, I recommend flashing the **.iso** of your OS in a USB stick.

**In the process of putting the OS into your USB, all the data inside of it will be wiped, make sure you make a proper backup in case you have anything important on it.**

To get the OS into your USB stick, I recommend using the tool called Balena Etcher. It works in both Windows and MacOS, and its free. https://www.balena.io/etcher/. 

Open Balena Etcher, select the .iso of your arch distro and USB stick, and then click on flash. it will take a while but eventually you will have your USB flashed and ready to use to install arch!.

### installing system from USB 
<!--This section is unfinished, make sure to detail the installation process better.-->

Make sure your flashed USB is plugged into your computer, then you have to restart into your boot menu, or BIOS to make sure you boot using your USB. This process is totally different from computer to computer, but the general idea is the same for most BIOS's out there.

Once you are in the Live enviroment, you can play with arch as much as you want, but understand that arch is not currently installed just yet. In the case that you are using RebornOS, there is a handy installer than will guide you through most of what you need.

<!--EXPLAIN HOW TO PARTITION-->

### Getting arch ready

Once you have arch installed, you can probably just boot into it using Grub or by changing the boot order in your BIOS.

First you have to know the following terms, which are going to be used throughout this guide:

Command | Definition
------------ | -------------
Install/Download| pacman -S **appname**
nano/edit | nano **name of file**

#### getting a custom kernel (OPTION)

There are multiple kernels in osu, you can pick whichever one you want, but I recommend using Linux-zen, since it is what ThePoon recommends and has worked most of the time for me.

``pacman -S linux-zen linux-zen-headers``

Once it is installed, you will have to update your grub for it to show it so you can access it. 

``grub-mkconfig -o /boot/grub/grub.cfg``

Once that finishes, you can restart and the linux-zen option will appear on the list to pick, when your computer boots you will be running Linux-zen!.

**If you use an nvidia gpu, make sure you install the nvidia-dkms driver, or else your computer wont boot on linux-zen.**

``pacman -S nvidia-dkms``

You can always read the wiki for more information.

#### Getting your video driver

Not all linux distributions come with the appropiate driver preinstalled. If you have an nvidia GPU you are most likely using Nouveau, which is NOT good for gaming and wouldn't advice using it.

To check which driver you are running:

``lspci -nnk``

    -01:00.0 VGA compatible controller [0300]: NVIDIA Corporation GP104 [GeForce GTX 1060 6GB] [10de:1b83] (rev a1)
	Subsystem: Gigabyte Technology Co., Ltd Device [1458:371a]
	Kernel driver in use: nvidia

Mine is currently the `nvidia` driver, but in case it is not, you can install it easily by doing

**For nvidia**

``pacman -S nvidia``

**For AMD**

``pacman -S amdgpu``

I don't personally own an AMD GPU, so I can't tell which driver is better, but the wiki might help you out better. https://wiki.archlinux.org/index.php/AMDGPU

#### Setting up your CPU governor

The CPU governor can have HUGE impact in performance, and not all cpus come with performance in mind. you can just change your governor to something that fits your needs better.

``pacman -S cpupower``

then to put the performance governor:

``cpupower frequency-set -g performance``

This will give you better performance not only in osu, but in your linux system overall.






