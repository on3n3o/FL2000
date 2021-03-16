arm_prefix = /opt/hi3798/arm-hisiv200-linux/bin/arm-hisiv200-linux-gnueabi

all:	driver

driver:	main.cpp
	g++ main.cpp -lX11 -ljpeg -o driver

driver_arm:	main.c
	$(arm_prefix)-g++ main.c -Xlinker -static -static-libgcc -o driver_arm
	$(arm_prefix)-strip driver_arm
