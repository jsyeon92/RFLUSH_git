# Makefile for BlueDBM
#

INCLUDE = ../../include
COMMON = ../../common
DEV_COMMON = ../common

EXTRA_CFLAGS := \
	-I$(PWD)/$(INCLUDE) \
	-I$(PWD)/$(COMMON)/utils \
	-I$(PWD)/$(COMMON)/3rd \
	-I$(PWD)/$(DEV_COMMON) \

EXTRA_CFLAGS += \
	-D CONFIG_ENABLE_MSG \
	-D CONFIG_ENABLE_DEBUG \
	-D CONFIG_DEVICE_TYPE_RAMDRIVE \
	-D KERNEL_MODE

dumbssd-y := \
	$(COMMON)/utils/ufile.o \
	$(COMMON)/utils/utime.o \
	$(COMMON)/utils/uthread.o \
	$(COMMON)/utils/umemory.o \
	$(DEV_COMMON)/dev_params.o \
	dev_hynix_nvme.o \
	dm_dumbssd.o \
	#$(DEV_COMMON)/dev_main.o \

obj-m := dumbssd.o

export KROOT=/lib/modules/$(shell uname -r)/build

.PHONY: default
default: modules

.PHONY: modules
modules:
	@$(MAKE) -C $(KROOT) M=$(PWD) modules
	@chmod +x dumbssd.ko

.PHONY: modules_check
modules_check:
	@$(MAKE) -C $(KROOT) C=2 M=$(PWD) modules

.PHONY: modules_install
modules_install:
	@$(MAKE) -C $(KROOT) M=$(PWD) modules_install

.PHONY: kernel_clean
kernel_clean:
	@$(MAKE) -C $(KROOT) M=$(PWD) clean
 
.PHONY: clean
clean: kernel_clean
	@$(RM) -rf Module.markers modules.order
	@cd ../common; $(RM) *.o

