#
# Copyright (C) 2011-2021 Intel Corporation. All rights reserved.
#
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions
# are met:
#
#   * Redistributions of source code must retain the above copyright
#     notice, this list of conditions and the following disclaimer.
#   * Redistributions in binary form must reproduce the above copyright
#     notice, this list of conditions and the following disclaimer in
#     the documentation and/or other materials provided with the
#     distribution.
#   * Neither the name of Intel Corporation nor the names of its
#     contributors may be used to endorse or promote products derived
#     from this software without specific prior written permission.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
# "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
# LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
# A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
# OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
# SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
# LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
# DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
# THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
# (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
# OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
#
#


include ../../buildenv.mk
ifndef VERBOSE
	PCLVERBOSE := @
else
	PCLVERBOSE := 
endif

INC_DIR	:= -I$(COMMON_DIR)/inc -I$(COMMON_DIR)/inc/internal -I.
CXXFLAGS += $(INC_DIR) -Wno-attributes -g -mrdrnd -fpie
LDFLAGS := -pie $(COMMON_LDFLAGS)

LINK_FLAGS := -lcrypto -L$(BUILD_DIR) -lsgx_tservice
CPP_FILES := encryptip.cpp
OBJS := $(CPP_FILES:.cpp=.o)
TOOL_NAME := sgx_encrypt

.PHONY: all

all: $(TOOL_NAME) | $(BUILD_DIR)
	$(PCLVERBOSE)$(CP) $< $|

$(BUILD_DIR):
	@$(MKDIR) $@

$(OBJS): $(CPP_FILES)
	$(PCLVERBOSE)$(CXX) -c $< -o $@ $(CXXFLAGS)
	@echo "CXX  =>  $@"

$(TOOL_NAME): $(OBJS)
	$(PCLVERBOSE)$(CXX) $^ -o $@ $(LINK_FLAGS) $(LDFLAGS)
	@echo "LINK =>  $@"

.PHONY: clean
clean:
	$(PCLVERBOSE)$(RM) $(TOOL_NAME) $(OBJS) $(BUILD_DIR)/$(TOOL_NAME)

.PHONY: rebuild
rebuild:
	$(MAKE) clean
	$(MAKE) all

