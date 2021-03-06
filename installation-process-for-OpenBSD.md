# OpenBSD 6.8 - Installation Notes
----------------------------
# A drafted installation process for OpenBSD (including WiFi, Gnome, ports and more)
###### [rosner][exo-mer], 2021-03-06T13:23:45Z

[install process](https://github.com/exo-mer/2021-research-os-OpenBSD/blob/main/installation-process-for-OpenBSD.md)

## preparing an installation media (USB stick)
The following steps are showing how to download and create a bootable usb stick. A General check for architecture and boot media are required (for this example the architecture is amd64 and installation media is a USB flash drive). Proceed to download an appropriate image (install68.img) and the SHA256, SHA256.sig files for later integrity checks.
### variant A - using curl
```
user $ curl -o install68.img https://cdn.openbsd.org/pub/OpenBSD/6.8/amd64/install68.img
user $ curl -o SHA256 https://cdn.openbsd.org/pub/OpenBSD/6.8/amd64/SHA256
```
### variant B - using wget
```
user $ wget https://cdn.openbsd.org/pub/OpenBSD/6.8/amd64/install68.img
user $ wget https://cdn.openbsd.org/pub/OpenBSD/6.8/amd64/SHA256
```
### check for integrity
The SHA256 file contains the checksums for all the installation files. Make use of sha256 / sha256sum depending on the OS of choice.
#### variant C - using BSD
```
user $ sha256 -C SHA256 install*.img
(SHA256) installXX.img: OK
```
#### variant D - using GNU coreutils (Linux)
```
user $ sha256sum -c --ignore-missing SHA256
installXX.img: OK
```

### verify and check for accidental corruption (OpenBSD)
```
$ signify -Cp /etc/signify/openbsd-XX-base.pub -x SHA256.sig install*.img
Signature Verified
installXX.img: OK
```

### identify and create the USB media
#### variant E (using disklabel - OpenBSD)
To identify the media the disklabel command is used.
```
root $ disklabel sd{0,1,2,3,4}
```
Being sure about the device file is essential to proceed with diskdump by using the identified device and the dd command.
```
root $ dd if=/path/to/install*.img of=/dev/rsd{0,1,2,3,4}c bs=1m
```
#### variant E (using cfdisk - GNU/Linux)
To identify the media the cfdisk or fdisk command can be used.
```
root $ cfdisk /dev/sd{a,b,c,d,e}
```
Being sure about the device file is essential to proceed with diskdump by using the identified device and the dd command.
```
root $ dd if=/path/to/install*.img of=/dev/sd{a,b,c,d,e} bs=1m
```
After running the diskdump without failures, the installation USB media is ready to boot from.

## booting from created media
By plugging in the USB stick the device will startup using OpenBSD.
### variant F (create a fully encrypted drive)
To create a fully encrypted drive proceed with section [RAID and Disk Encryption](https://www.openbsd.org/faq/faq14.html) from [OpenBSD](https://www.openbsd.org/) directly.
### variant G (make use of fully encrypted drive)
Sometimes there is a fully encrypted drive present already. To make use of such a drive create device nodes first (make sure to create some more in addition to further usage; depending on the number of disk drives). Using the (S) shell option will lead to (one might want to use dmsg to gather information on disk drives).
#### creating device nodes in dev
Creating the missing device nodes is done by running the following (four nodes are created for later purpose).
```
root $ cd /dev
root $ sh MAKEDEV sd0
root $ sh MAKEDEV sd1
root $ sh MAKEDEV sd2
root $ sh MAKEDEV sd3
```

#### unlock the disk
Using disklabel will help to identify the drive. Unlocking the disk will then be done using the bioctl command and the correctly proviced passphrase or key instead - this example deals with a passphrase.
```
root $ disklabel sd{0,1,2,3}			# use one integer to identify the drive
root $ bioctl -c C -l sd{0,1,2,3} softraid0	# use the identified integer for suited drive
```
After unlocking the drive a sdX will be assigned to the drive as new device node. Unlocking the drive is complete. Remembering the assigned sdX will help in the further installation process. Leaving the shell is done with the exit command.
```
root $ exit
```
## installation
Proceeding with the installation is not that hard. Making good choices is supported by several sources - details in:
+ [OpenBSD 5.5 Installation Notes](https://ijsbeer.org:81/openbsd-55-installation-notes.html)
+ [OpenBSD 6.8 FAQ - Installation Guide](https://www.openbsd.org/faq/faq4.html) 
To succeed with the installation process it is important to remember the sdX {sd0,sd1,sd2,sd3,..} from the section above (unlock the disk).
After the installation has finished a (R) reboot will assure a first login to the new system - remembering the root / user's passphrase.

### update the system with firmware and patches
Updating the firmware and providing patches will be quickly achieved by running this commandline as root user.
```
root $ fw_update && syspatch && reboot
```
A reboot is neccessary - and booting into the updated system will be done; so new login is next.

### WiFi
To check for current network devices using dmesg is a good choice.
```
root $ dmesg | grep 'iwn0'
```
Adding a network will be done with an echo as root.
```
root $ echo 'join THE-ESSID wpakey WITH-THIS-KEY' >> /etc/hostname.iwn0
root $ chmod 640 /etc/hostname.iwn0
root $ sh /etc/netstart
```
In a good environment, performing these steps will lead to a wireless connection.

## adding Gnome
Having a GUI is nice! - by adding these packages, the Gnome environment will be installed.
```
root $ pkg_add gnome gnome-extra gdm chromium nano
root $ rcctl xenodm
root $ rcctl enable multicast messagebus avahi_daemon gdm
root $ usermod -G staff USER
root $ rcctl start messagebus
```
And the USER be added to the staff group. By altering the login.conf the memory limits can be changed individually to each machines memory.
```
root $ nano /etc/login.conf	# edit staff section > datasize-cur = 8192; maxproc-max = 2048; maxproc-cur = 1024
```
## power management
Having the lid close leading to suspension is great.
```
root $ echo 'apmd_flags="-A -z 10"' >> /etc/rc.conf.local	# suspend with 10% battery power
root $ echo 'machdep.lidaction=1' >> /etc/sysctl.conf		# 1 for suspend, 2 for hibernate
root $ rcctl start apmd
```

## ports
Binary packages are great - sometimes building packages is prefered. To get the ports for the current release running will work.
```
user $ cd /tmp
user $ ftp https://cdn.openbsd.org/pub/OpenBSD/$(uname -r)/{ports.tar.gz,SHA256.sig}
user $ signify -Cp /etc/signify/openbsd-$(uname -r | cut -c 1,3)-base.pub -x SHA256.sig ports.tar.gz
```
After fetching the tar package changing to root user is needed to unpack the ports tree to the /usr directory.
```
root $ cd /usr
root $ tar xzf /tmp/ports.tar.gz
```
Initially changing the /etc/mk.conf might be desired to build packages.
```
root $ echo 'WRKOBJDIR=/usr/obj/ports' >> /etc/mk.conf
root $ echo 'DISTDIR=/usr/distfiles' >> /etc/mk.conf
root $ echo 'PACKAGE_REPOSITORY=/usr/packages' >> /etc/mk.conf
root $ cat /etc/mk.conf
```
Now it should be possible to build packages using ports.

After adding the portslist package -
```
root $ cd /usr/ports
root $ pkg_add portslist
```
searching ports will work as the following shows.
```
root $ make search key=gcc
```

## build gcc
To build and install the GNU Compiler Collection changing the directory and some tea is required.
```
root $ cd /usr/ports/lang/gcc
root $ make
root $ make install
```
After the compilation has finished - the software will be installed to directories accordingly (gcc, g++, g95 - checking the documentation for binaries might be helpful). 
 
###### Thanks for your visit!
###### If you like this document, consider to share the url above or give it a star.
###### Enjoy reading.

##### Sources
+ [OpenBSD - FAQ Installation Guide](https://www.openbsd.org/faq/faq4.html)
+ [OpenBSD - RAID and Disk Encryption](https://www.openbsd.org/faq/faq14.html)
+ [OpenBSD - manual page server](https://man.openbsd.org/man)
+ [OpenBSD on wikibooks](https://de.wikibooks.org/wiki/OpenBSD/_Systemprogramme)
+ [Keith Burnett - Running OpenBSD 6.8 on your laptop is really hard (not)](https://sohcahtoa.org.uk/openbsd.html)
+ [Rob Crowther - OpenBSD 5.5 Installation Notes](https://ijsbeer.org:81/tag/openbsd.html)
