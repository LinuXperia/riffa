# ----------------------------------------------------------------------
# Copyright (c) 2016, The Regents of the University of California All
# rights reserved.
# 
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are
# met:
# 
#     * Redistributions of source code must retain the above copyright
#       notice, this list of conditions and the following disclaimer.
# 
#     * Redistributions in binary form must reproduce the above
#       copyright notice, this list of conditions and the following
#       disclaimer in the documentation and/or other materials provided
#       with the distribution.
# 
#     * Neither the name of The Regents of the University of California
#       nor the names of its contributors may be used to endorse or
#       promote products derived from this software without specific
#       prior written permission.
# 
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL REGENTS OF THE
# UNIVERSITY OF CALIFORNIA BE LIABLE FOR ANY DIRECT, INDIRECT,
# INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING,
# BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS
# OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
# ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR
# TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE
# USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH
# DAMAGE.
# ----------------------------------------------------------------------
#-----------------------------------------------------------------------
# Filename:            Makefile
# Version:             1.0
# Description:         Top-level makefile for building all vendor projects
# Author:              Dustin Richmond (@darichmond)
#-----------------------------------------------------------------------

CURRENT_PATH := $(patsubst %/,%,$(dir $(abspath $(lastword $(MAKEFILE_LIST)))))
CURRENT_DIR := $(shell basename $(CURRENT_PATH))
RIFFA_ROOT_PATH:=$(CURRENT_PATH)/..
RIFFA_HDL_PATH:=$(RIFFA_ROOT_PATH)/$(CURRENT_DIR)/riffa_hdl
include $(RIFFA_ROOT_PATH)/release.mk
.DEFAULT_GOAL := all
VENDORS:= altera xilinx 
SUBDIRS = $(VENDORS)

all classic: $(VENDORS)

ultrascale: check-hdl
	$(MAKE) -C xilinx $(MAKECMDGOALS) RIFFA_HDL_PATH=$(RIFFA_HDL_PATH) RIFFA_ROOT_PATH=$(RIFFA_ROOT_PATH)

$(VENDORS):: check-hdl
	$(MAKE) -C $@ $(MAKECMDGOALS) RIFFA_HDL_PATH=$(RIFFA_HDL_PATH) RIFFA_ROOT_PATH=$(RIFFA_ROOT_PATH)

clean-release:check-release-src
	rm -rf $(RELEASE_SRC_PATH)/$(CURRENT_DIR)

destination: $(RELEASE_SRC_PATH)/fpga

$(RELEASE_SRC_PATH)/fpga: check-release-src
	mkdir $@

release: check-release-src destination $(VENDORS)
	cp -r $(CURRENT_PATH)/riffa_hdl $(RELEASE_SRC_PATH)/$(CURRENT_DIR)
	rm -r $(RELEASE_SRC_PATH)/$(CURRENT_DIR)/riffa_hdl/riffa.mk

.PHONY:clean $(SUBDIRS) clobber release

clean clobber: $(VENDORS)
	rm -rf *~ *.jou *.log








