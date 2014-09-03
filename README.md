## MT7601U Linux driver

Many cheap USB wifi dongles use the MT7601U chip

<img src="http://porjo.github.io/mt7601/dongle1.jpg" width="150">
<img src="http://porjo.github.io/mt7601/dongle2.jpg" width="150">

Unfortunately, the driver is not part of the Linux kernel source tree (yet?). This repository contains:
* source code from [DPO_MT7601U_LinuxSTA_3.0.0.4_20130913.tar.bz2](http://www.mediatek.com/en/downloads/mt7601u-usb/) (md5sum 5f440dccc8bc952745a191994fc34699) 
* patched with code from http://www.spinics.net/lists/linux-wireless/msg126291.html

The patch improves stability and performance for kernels >= 3.x

### Usage

First install kernel-devel for your Linux distro

```
git clone https://github.com/porjo/mt7601.git
cd mt7601/src
make
sudo insmod os/linux/mt7601Usta.ko
```

If the module has loaded OK, you should see `mt7601Usta` listed in the output of `lsmod` and a new network interface `ra0` should be present in the output of `ip link`

### History

On 26 Aug, 2014 user **@poma** posted to the [linux-wireless](http://wireless.kernel.org/en/developers/MailingLists) mailing list discussing the poor state of driver support for this chipset. Thread can be seen here:

http://www.spinics.net/lists/linux-wireless/msg126115.html

An inital patch was released on 28 Aug, 2014 with the following comment:
```
A patch[1] is composed partly from the RT3573 source code patched by ashaffer, from Andreas work, some of the ideas are from the beagleboard community, and some of my. :)
Debug(trace) is turned off.

Device now works more or less OK but slow, max. 10 Mbit, although connectable is only within the "N" & "N/G" modes.
What is important is the system no longer crashes, and disconnection are rare.
Generally better than before.

Tested with kernels:
3.15.10-200.fc20.x86_64
3.16.1-301.fc21.x86_64
3.17.0-0.rc2.git0.1.fc22.x86_64

and with debug kernel:
3.17.0-0.rc2.git1.1.fc22.x86_64
```

A second patch was released on 31 Aug, 2014 with the following comment:

```
A new patch[1] mainly based on patches at 
https://github.com/ashaffer/rt3573sta
and several network throughput tests via the Iperf.
Tested with kernels:
- 3.15.10-200.fc20.x86_64
- 3.16.1-301.fc21.x86_64
- 3.17.0-0.rc2.git3.1.fc22.x86_64
- 3.16.1-301.fc21.i686
- 3.17.0-0.rc2.git3.1.fc22.i686
```



### Credits

**Source code:** (c) Copyright 2002-2013, MediaTek Inc. (released under GPLv2)

**Patch:** @goma at [linux-wireless](http://wireless.kernel.org/en/developers/MailingLists) mailing list
