arch-kali-pogoplug
==================

The build scripts for Kali image of Pogoplug,
runing on Debian or Arch Linux.


Build
-----

You may compile the kali image in one step:

    git clone https://github.com/yhfudev/arch-kali-pogoplug.git
    cd arch-kali-pogoplug
    sudo ./runme.sh

You may want to run above commands in a virtual machine by user root,
otherwise you may be annoyed by the sudo command :-)

Install
-------
TODO

Config
------
You may be also interest in config or install other packages after booting the Kali:
(user "root" login with password "toor")

    # expanded the image to the full size
    apt-get install parted sudo
    /scripts/rpi-wiggle.sh
    
    # Full Kali Linux build
    apt-get update
    apt-get install kali-linux-full
    
    # setup ssh server
    apt-get install openssh-server
    update-rc.d -f ssh remove
    update-rc.d -f ssh defaults
    rm /etc/ssh/ssh_host_*
    dpkg-reconfigure openssh-server
    service ssh restart

Features
--------

* Supports the PogoPlug E02/v4
* automatically download and install prerequisites
* automatically download, setup, and cache source/tool trees
* Supports dpkg cache, so you won't wait after the first run of this software
* Supports multiple linux distributions, such Debian, Arch (or Redhat, not test yet)

That's all. Have fun!
