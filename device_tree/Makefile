PLATFORM_NAME=kv260_custom

ROOT_DIR=$(realpath $(dir $(lastword $(MAKEFILE_LIST))))
BUILD_PATH=$(ROOT_DIR)/build
VERSION ?=2024.2
XSA_NAME=kv260_hardware_platform

DTB_BUILD_PATH=$(BUILD_PATH)/dtb
DT_PLAT_NAME=mydeivice
DT_PATH=$(DTB_BUILD_PATH)/$(DT_PLAT_NAME)/psu_cortexa53_0/device_tree_domain/bsp

USER_DTSI=system-user_dma2_dma2.dtsi

all: dtb dtbo

dtb:
	@echo "execute createdts to generate dtb file"
#	xsct -eval " hsi::open_hw_design $(ROOT_DIR)/../hardware_design/build/vivado/$(XSA_NAME).xsa "
	xsct -eval " createdts -hw $(ROOT_DIR)/../hardware_design/build/vivado/$(XSA_NAME).xsa -zocl -platform-name $(DT_PLAT_NAME) -git-branch xlnx_rel_v$(VERSION) -overlay -compile -out $(DTB_BUILD_PATH) " 
#   -dtsi system-user.dtsi

dtbo: $(DT_PATH)/pl.dtsi
	cp $(USER_DTSI) $(DT_PATH)/

#	dtc -@ -O dtb -o $(DT_PATH)/pl.dtbo $(DT_PATH)/pl.dtsi
	dtc -@ -O dtb -o $(DT_PATH)/pl.dtbo $(DT_PATH)/$(USER_DTSI)

	cp $(DT_PATH)/pl.dtbo $(DTB_BUILD_PATH)/