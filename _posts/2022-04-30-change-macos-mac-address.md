---
title: How to change the MAC address of an interface on MacOS?
excerpt_separator: <!--end_excerpt-->
---

This tutorial explains how to change the MAC address/physical adress of an network interface on MacOS.
<!--end_excerpt-->

Step 1: Make sure your interface is disconnected.

If your network connection is active, you will get the following error:

```
ifconfig: ioctl (SIOCAIFADDR): Can't assign requested address
```

Step 2:

Open **Terminal** and type:
```
sudo ifconfig en0 ether 12:34:56:78:90:ab
```
where:
- en0 is the name of the interface
- 12:34:56:78:90:ab is the desired MAC address
