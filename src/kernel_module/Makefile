# ---------------------------------------------------------------------------
# dma_proxy — out-of-tree kernel module
# ---------------------------------------------------------------------------
#  ❱ Native build ..............  $ make
#  ❱ Cross-compile for ZynqMP ..  $ make ARCH=arm64 \
#                                     CROSS_COMPILE=aarch64-linux-gnu- \
#                                     KERNEL_SRC=/opt/linux-xlnx-5.15
# ---------------------------------------------------------------------------

# Path to the *prepared* kernel tree you want to build against.
#  * Native default = running kernel headers.
#  * Override for cross-compilation.
KERNEL_SRC ?= /lib/modules/$(shell uname -r)/build

# Cross-compiler triplet (leave empty for native).
CROSS_COMPILE ?=
ARCH          ?= $(shell uname -m)   # overridden automatically by CROSS_COMPILE

# Header directory you want on the module’s include path
INC := $(PWD)/../Software/Common
ccflags-y := -I$(INC)                # ccflags-y is preferred over EXTRA_CFLAGS

obj-m := dma_proxy.o

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