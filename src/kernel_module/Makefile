# ---------------------------------------------------------------------------
# dma_proxy — out-of-tree kernel module
# ---------------------------------------------------------------------------
#  ❱ Native build ..............  $ make
#  ❱ Cross-compile for ZynqMP ..  $ make ARCH=arm64 \
#                                     CROSS_COMPILE=aarch64-linux-gnu- \
#                                     KERNEL_SRC=/opt/linux-xlnx-5.15
# ---------------------------------------------------------------------------

# Cross-compiler triplet (leave empty for native).
CROSS_COMPILE ?=
ARCH          ?= $(shell uname -m)   # overridden automatically by CROSS_COMPILE
SYSROOT       ?=  $(SDKTARGETSYSROOT)        # e.g. /opt/petalinux/2023.2/sysroots/aarch64

# Path to the *prepared* kernel tree you want to build against.
#  * Native default = running kernel headers.
#  * Override for cross-compilation.
#KERNEL_SRC ?= $(SYSROOT)/lib/modules/$(shell uname -r)/build
#KERNEL_SRC ?= $(SYSROOT)/lib/modules/6.6.40-xilinx-g2b7f6f70a62a/build
KERNEL_SRC = /home/emanuel/workspace/xilinx-zynqmp-common-v2024.2/sysroots/sysroots/cortexa72-cortexa53-xilinx-linux/lib/modules/6.6.40-xilinx-g2b7f6f70a62a/build

# Header directory you want on the module’s include path
INC := $(PWD)/../common
ccflags-y := -I$(INC)                # ccflags-y is preferred over EXTRA_CFLAGS

obj-m := dma-proxy.o

# ---------------------------------------------------------------------------
# Targets
# ---------------------------------------------------------------------------
all:
	$(MAKE) -C $(KERNEL_SRC) \
	        ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) \
	        M=$(PWD) modules

clean:
	$(MAKE) -C $(KERNEL_SRC) \
	        ARCH=$(ARCH) CROSS_COMPILE=$(CROSS_COMPILE) \
	        M=$(PWD) clean


#INC = /home/ubuntu/Programming/software-prototypes/linux-user-space-dma/Software/Common/
#EXTRA_CFLAGS += -I$(INC)

#obj-m += dma_audio_driver.o
#all:
#    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
#clean:
#    make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean