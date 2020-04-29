# Driver for FL2000

> possible best answer https://stackoverflow.com/questions/24988164/c-fast-screenshots-in-linux-for-use-with-opencv/39781697

1. Add Virtual1 display as said here https://unix.stackexchange.com/questions/378373/add-virtual-output-to-xorg
2. Enable output on virtual1 as said here 

Generate modeline and add to virtual1
cvt $width $height $fps
cvt 1280 1024 60
xrandr --newmode "1280x1024_60.00" 109.00  1280 1368 1496 1712  1024 1027 1034 1063 -hsync +vsync
xrandr --addmode VIRTUAL1 "1280x1024_60.00"
# display will blink here, check display position in [Windows key] => displays
# you can see display preview in OBS
xrandr --output VIRTUAL1 --mode "1280x1024_60.00" 

# Fresco Logic FL2000 Linux/Android kernel driver (ORIGINAL DESCRIPTION BELOW)

### 1. What is this?

This is an official driver release from Fresco Logic in an attempt to help the open-source community adopting the development and use of the FL2000DX device.
This driver only covers the USB part of the display logic. It does not support the Linux desktop logic (eg. extended desktop vs mirrored desktop).

### 2. On which kernel versions does this driver work?

This driver is tested on Ubuntu 14 LTS as well as some Android platforms with kernel version 3.10.x.
This driver source might not compile on newer kernels (eg. 4.0 or above) because of the fast-moving API changes in the
mainstream kernel. You might need to adapt it for your own use.

### 3. Target audience

This release is targeted to open-source developers, as opposed to end-users.

### 4. How do I enable extended desktop/mirrored desktop on my X Window?

Currently Fresco Logic does not provide desktop related manipulation.
Fresco Logic hopes the community will contribute to this area so that end-users can easily adopt this solution.

### 5. FL2000DX limitation.

The FL2000DX chip is cheap by design where it doesn't have a frame buffer on its own.
It relies heavily on USB 3.0 transfer speed to accommodate continuous USB flow.
The larger the image is, the heavier it depends on USB bandwidth.
A typical 1920x1080@60 Hz requires 1920 * 1080 * 24bpp * 60 = 373,248,000 bytes/sec of traffic over the USB bus.
As such, USB2.0 speed is not supported.

Connecting more than one FL2000DX device to the same bus is deprecated.

### 6. How do I compile & test the kernel driver?
#### 6a. Compile the driver

Find your kernel source tree, and edit `src/Makefile`. Locate the following line:
    
    KERNEL_PATH = /usr/src/linux-headers-4.4.0-72-generic`
    
Modify this line so that it points to the correct source tree.
After that, run `make` to create `fl2000.ko` and run `insmod fl2000.ko` to load the driver.

#### 6b. Test the driver

In the `sample` folder, run `make` to create `fltest`. If you you are using a
cross compiler to build the binary for specific platforms, you need to specify that specific
compiler in `src/Makefile`.
    
Run `./fltest 0` as superuser to run the test. The driver provides several
user mode buffer access methods (e.g  copy to kernel internal buffer, or
directly locking down user buffer). Look at `fl2000_ioctl.h` for detailed
information.

### 7. How do I file a bug to the Fresco Logic developers?

You can file bugs to [Github Issues](https://github.com/fresco-fl2000/fl2000/issues)



