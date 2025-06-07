# ---------------------------------------------------------------------------
#  dma-proxy-test – user-space benchmark
#
#  Native build ……………  $ make
#  Cross build …………   $ make CROSS_COMPILE=aarch64-linux-gnu- \
#                            SYSROOT=/opt/petalinux/sysroots/aarch64  \
#                            BUILD_DIR=build-aarch64
# ---------------------------------------------------------------------------

# ------------  configurable knobs  -----------------------------------------
CROSS_COMPILE ?= 
SYSROOT       ?= $(SDKTARGETSYSROOT)
BUILD_DIR     ?= build
INC_DIR       ?=                       # add -I path here if dma-proxy.h is elsewhere
TARGET        := $(BUILD_DIR)/dma-proxy-test
SRCS          := dma-proxy-test.c
OBJS          := $(addprefix $(BUILD_DIR)/,$(SRCS:.c=.o))

CC      := $(CROSS_COMPILE)gcc
CFLAGS  := -Wall -O3 -std=gnu11 -pthread -I../common
LDFLAGS := -pthread
ifeq ($(strip $(INC_DIR)),)
else
CFLAGS  += -I$(INC_DIR)
endif
ifeq ($(strip $(SYSROOT)),)
else
CFLAGS  += --sysroot=$(SYSROOT)
LDFLAGS += --sysroot=$(SYSROOT)
endif
# ---------------------------------------------------------------------------

.PHONY: all clean dirs

all: $(TARGET)

# Create the out-of-tree build directory once
dirs: ; @mkdir -p $(BUILD_DIR)

# Pattern rule: build/<file>.o from <file>.c
$(BUILD_DIR)/%.o: %.c | dirs
	$(CC) $(CFLAGS) -c $< -o $@

# Final link step
$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $@ $^ $(LDFLAGS)
	@echo "Built $@"

clean:
	@rm -rf $(BUILD_DIR)
