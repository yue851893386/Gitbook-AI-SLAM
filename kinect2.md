---
title: This is the Study Notes of Kinect2
---


## Install Driver
- [Driver-OpenKinect/libfreenect2](https://github.com/OpenKinect/libfreenect2)
- **My Environment**
```bash
yubao@yubao-Z370M-S01:~/GoogleDrive$ uname -a
Linux yubao-Z370M-S01 4.15.0-42-generic \#45~16.04.1-Ubuntu SMP Mon Nov 19 13:02:27 UTC 2018 x86_64 x86_64 x86_64 GNU/Linux
```

**Errors when install libfreenect2**

It tooks me one night to solve this error:
- Error description

kinect run error:Wrong JPEG library version

```sh
yubao@yubao-Z370M-S01:~/Software/libfreenect2$ ./build/bin/Protonect
Version: 0.2.0
Environment variables: LOGFILE=<protonect.log>
Usage: ./build/bin/Protonect [-gpu=<id>] [gl | cl | clkde | cuda | cudakde | cpu] [<device serial>]
        [-noviewer] [-norgb | -nodepth] [-help] [-version]
        [-frames <number of frames to process>]
To pause and unpause: pkill -USR1 Protonect
[Info] [Freenect2Impl] enumerating devices...
[Info] [Freenect2Impl] 8 usb devices connected
[Info] [Freenect2Impl] found valid Kinect v2 @2:3 with serial 006696152647
[Info] [Freenect2Impl] found 1 devices
Wrong JPEG library version: library is 90, caller expects 80
```

- Solution
[refer](https://github.com/OpenKinect/libfreenect2/issues/1004)
```sh
conda install jpeg=8
```
Remember to rebuild libfreenect2.

## Test Kinect2
**Run:**
```bash
(base) yubao@yubao-Z370M-S01:~/Software/libfreenect2/build$ ./bin/Protonect
Version: 0.2.0
Environment variables: LOGFILE=<protonect.log>
Usage: ./bin/Protonect [-gpu=<id>] [gl | cl | clkde | cuda | cudakde | cpu] [<device serial>]
        [-noviewer] [-norgb | -nodepth] [-help] [-version]
        [-frames <number of frames to process>]
To pause and unpause: pkill -USR1 Protonect
[Info] [Freenect2Impl] enumerating devices...
[Info] [Freenect2Impl] 8 usb devices connected
[Info] [Freenect2Impl] found valid Kinect v2 @2:3 with serial 006696152647
[Info] [Freenect2Impl] found 1 devices
libva info: VA-API version 0.39.0
libva info: va_getDriverName() returns -1
libva error: va_getDriverName() failed with unknown libva error,driver_name=(null)
[Error] [VaapiRgbPacketProcessorImpl] vaInitialize(display, &major_ver, &minor_ver): unknown libva error
[Info] [Freenect2DeviceImpl] opening...
[Info] [Freenect2DeviceImpl] transfer pool sizes rgb: 20*16384 ir: 60*8*33792
```

**Result:**

![Kinetic2 Demo](../Assets/Images/Kinetic2_Protonect_Test_Result.jpg)


## Ros Simulation - iai_kinect2
- [github](https://github.com/code-iai/iai_kinect2)
-
