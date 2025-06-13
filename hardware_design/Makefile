#/*
#Copyright (C) 2023, Advanced Micro Devices, Inc. All rights reserved.
#SPDX-License-Identifier: MIT
#*/

ROOT_DIR=$(realpath $(dir $(lastword $(MAKEFILE_LIST))))
ABS_BUILD_PATH=$(ROOT_DIR)/build
ABS_HW_PATH=$(ABS_BUILD_PATH)/vivado
VERSION ?=2024.2
BD_TCL=block_design_dma_fifo_dma_$(VERSION).tcl
ABS_BD_TCL=$(ROOT_DIR)/$(BD_TCL)
XSA_TCL=export_xsa_$(VERSION).tcl
ABS_XSA_TCL=$(ROOT_DIR)/$(XSA_TCL)

.PHONY: help

help:
	@echo "Makefile usage"
	@echo "make all 	## Generate hw platform and export XSA file"

all: hw

hw:
	mkdir -p $(ABS_HW_PATH)
	cd $(ABS_HW_PATH); vivado -mode batch -notrace -source $(ABS_BD_TCL) -source $(ABS_XSA_TCL)

clean:
	$(RM) -r build