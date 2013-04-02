Lightwerk ievms
===============

This is a modified version of the great ievms script by [xdissent](https://github.com/xdissent/ievms).

It will automatically set you up with a testing cluster of IE7, IE8, IE9 and IE10 with enabled RDP.

The VMs will run out of license after 90 days. Just re-run this script and we will reset (re-install) your VMs without additional download.

Modifications
-------------
* we kicked IE6 ... really no need for that anymore!
* we brought IE7 / IE8 to WinXP and IE9 / IE10 to Win7
** this reduces download (17 G -> 5.5 G) and diskspace (74 G -> 28.6 G)
* we introduced REFRESH=TRUE to reset the VMs
* we clean up our mess right after installing

Overview
========

Microsoft provides virtual machine disk images to facilitate website testing in multiple versions of IE, regardless of the host operating system. 

The [MS images](http://www.modern.ie/virtualization-tools) are fully compatible with Virtualbox, thanks to the [modern.IE](http://modern.IE) project.

[![Click here to lend your support to ievms and make a donation at pledgie.com!](http://pledgie.com/campaigns/15995.png?skin_name=chrome)](http://pledgie.com/campaigns/15995)


Quickstart
==========

Just paste this into a terminal: `curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | bash`


Requirements
============

* VirtualBox (http://virtualbox.org)
* Curl (Ubuntu: `sudo apt-get install curl`)
* Linux Only: unar (Ubuntu: `sudo apt-get install unar`)
* Patience


Disk requirements
-----------------

A full ievms install will require approximately 37G:

    Servo:.ievms lw$ du -ch *
     10G  IE10 - Win7-disk1.vmdk
    724M  IE6 - WinXP.ova
    1.6G  IE7 - WinXP-disk1.vmdk
     15M  IE7-WindowsXP-x86-enu.exe
    1.6G  IE8 - WinXP-disk1.vmdk
     16M  IE8-WindowsXP-x86-ENU.exe
     10G  IE9 - Win7-disk1.vmdk
    4.7G  IE9 - Win7.ova
    3.4M  ievms-control.iso
    4.6M  lsar
    4.5M  unar
    4.1M  unar1.5.zip
     28G  total
   
We do the auto-cleanup for you, so you should just keep the files in their place. That way we don't have to download anything to reset your VMs.


Installation
============

1. Install VirtualBox (make sure command line utilities are selected and installed).

2. Download and unpack ievms:

   * Install IE versions 7, 8, 9 and 10.

        curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | bash

   * Install specific IE versions (IE7 and IE9 only for example):

        curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | IEVMS_VERSIONS="7 9" bash

    * Re-Install all your expired VMs (you will lose all stored data)

        curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | IEVMS_VERSIONS="7 9" REFRESH=TRUE bash

3. Start all your VMs

        curl -s https://raw.github.com/lightwerk/ievms/master/runAll.sh | bash


Recovering from a failed installation
-------------------------------------

Each version is installed into `~/.ievms/` (or `INSTALL_PATH`). If the installation fails
for any reason (corrupted download, for instance), delete the appropriate ZIP/ova file
and rerun the install.

If nothing else, you can delete `~/.ievms` (or `INSTALL_PATH`) and rerun the install.


Specifying the install path
---------------------------

To specify where the VMs are installed, use the `INSTALL_PATH` variable:

    curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | INSTALL_PATH="/Path/to/.ievms" bash


Passing additional options to curl
----------------------------------

The `curl` command is passed any options present in the `CURL_OPTS` 
environment variable. For example, you can set a download speed limit:

    curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | CURL_OPTS="--limit-rate 50k" bash


Features
========

Clean Snapshot
--------------

A snapshot is automatically taken upon install, allowing rollback to the
pristine virtual environment configuration. Anything can go wrong in 
Windows and rather than having to worry about maintaining a stable VM,
you can simply revert to the `clean` snapshot to reset your VM to the
initial state.


RDP
---

Every VM is enabled with RDP. The network is configured to not pollute your network, so the VMs only get internal IPs. Just use the host to connect 
to RDP. The port is determined by the IE version (IE7 -> 6007, IE9 -> 6009, IE10 -> 6010).

You can change the first two digist by specifying PORT_PREFIX. 

    curl -s https://raw.github.com/lightwerk/ievms/master/ievms.sh | PORT_PREFIX="55" bash

Acknowledgements
================

* [xdissent](https://github.com/xdissent/ievms) - Creator of the original ievms scripts
* [modern.IE](http://modern.ie) - Provider of IE VM images.
* [ntpasswd](http://pogostick.net/~pnh/ntpasswd/) - Boot disk starting point
and registry editor.
* [regit-config](https://github.com/regit/regit-config) - Minimal Virtualbox
kernel config reference.
* [uck](http://sourceforge.net/projects/uck/) - Used to (re)master control ISO.

License
=======

As xdissent has not given any license yet, let's just hope he will not sue us. I can therefor not provide a license at the moment.
