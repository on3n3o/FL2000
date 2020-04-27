arm_prefix = /opt/hi3798/arm-hisiv200-linux/bin/arm-hisiv200-linux-gnueabi

all:	driver

driver:	main.c
	gcc main.c -o driver

driver_arm:	main.c
	$(arm_prefix)-gcc main.c -Xlinker -static -static-libgcc -o driver_arm
	$(arm_prefix)-strip driver_arm
