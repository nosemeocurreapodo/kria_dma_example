# -----------------------------------------------------------------------------
#CROSS_COMPILE ?=          # e.g. aarch64-linux-gnu-
SYSROOT       ?=  $(SDKTARGETSYSROOT)        # e.g. /opt/petalinux/2023.2/sysroots/aarch64

# -----------------------------------------------------------------------------
# Toolchain & flags
# -----------------------------------------------------------------------------

CC      := $(XILINX_VITIS)/gnu/aarch64/lin/aarch64-linux/bin/aarch64-linux-gnu-gcc
#CC      := $(CROSS_COMPILE)gcc
TARGET  := dma-proxy-test
SRCS    := dma-proxy-test.c
OBJS    := $(SRCS:.c=.o)

# Where dma-proxy.h lives if it is NOT in the same directory.
# Leave empty or set INC_DIR=/some/path when you invoke make.
INC_DIR ?= ../common

CFLAGS  := -Wall -O3 -std=gnu11 -pthread
ifeq ($(strip $(INC_DIR)),)
else
CFLAGS  += -I$(INC_DIR)
endif
ifeq ($(strip $(SYSROOT)),)
else
CFLAGS  += --sysroot=$(SYSROOT)
LDFLAGS += --sysroot=$(SYSROOT)
endif

LDFLAGS += -pthread

# -----------------------------------------------------------------------------
# Rules
# -----------------------------------------------------------------------------
all: $(TARGET)

$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS)

%.o: %.c
	$(CC) $(CFLAGS) -c -o $@ $<

clean:
	@$(RM) $(OBJS) $(TARGET)

.PHONY: all clean