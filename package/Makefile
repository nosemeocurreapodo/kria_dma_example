PACKAGE_PATH=$(PWD)/package

all: $(PACKAGE_PATH)

create_json:
	cd $(BUILD_PATH) && printf '{\n  "shell_type" : "XRT_FLAT",\n  "num_slots": "1"\n}' > shell.json

$(PACKAGE_PATH): create_json
	@echo "INFO: Packaging Completed"
	mkdir -p $(PACKAGE_PATH)
	cp ../device_tree/build/dtb/pl.dtbo $(PACKAGE_PATH)/dma-proxy.dtbo
	printf '{\n  "shell_type" : "XRT_FLAT",\n  "num_slots": "1"\n}' > $(PACKAGE_PATH)/shell.json
	cp ../hardware_design/build/vivado/kv260_hardware_platform.bit $(PACKAGE_PATH)/dma-proxy.bit
	cp ../src/userspace_code/build/dma-proxy-test $(PACKAGE_PATH)
#	cp ../src/kernel_module/build/dma-proxy.ko $(PACKAGE_PATH)
	@echo "Please  copy $(PACKAGE_PATH) to /lib/firmware/xilinx/ on target board"
	@echo "then use xmutil to load hardware."
	@echo "xmutil unloadapp"
	@echo "xmutil loadapp dma-proxy"
	@echo "then load the kernel module"
	@echo "sudo insmod dma-proxy.ko"
	@echo "Go to /lib/firmware/xilinx/dma-proxy directory and run application"
	@echo "$ ./dma-proxy-test "