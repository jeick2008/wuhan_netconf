
include  $(TOP_DIR)/build/env.rule

SRC_DIR=libnetconf-master

.PHONY:all clean

CURRENT_DIR = $(shell pwd)
LOCAL_INSTALL_LIB_DIR = $(CURRENT_DIR)/install
SBIN=ipset

CROSS_HOST = $(HOST) 
LIBXML2_INC_PATH = $(TOP_DIR)/libxml2/libxml2-master/libltdl/libltdl
LIBXML2_LIB_PATH = $(TOP_DIR)/apps/gpl/appkgs/libtool-1.0.4/install/lib
LIBXML2_BUILD_PATH = $(TOP_DIR)/libxml2

CONFIG_CMD = ./configure --prefix=$(LOCAL_INSTALL_LIB_DIR) --host=$(CROSS_HOST) --enable-static  libxml2_CFLAGS=-L$(LIBXML2_LIB_PATH)\ -I$(LIBXML2_INC_PATH) libxml2_LIBS=-lxml2  PKG_CONFIG_PATH=$(WINDRIVER_BASE)/gnu/4.1.2-vxworks-6.6/x86-linux2/powerpc-wrs-vxworks/bin/ CC=$(CC) --oldincludedir=$(C_INCLUDE_PATH)/wrn/coreip/


all: 
	@if [ ! -d $(SRC_DIR) ]; then \
	    echo "Untarring original $(SRC_DIR) source"; \
	    (unzip $(SRC_DIR).zip 2> /dev/null || true); \
	    mkdir -p $(LOCAL_INSTALL_LIB_DIR); \
	    cd $(CURRENT_DIR)/$(SRC_DIR) && $(CONFIG_CMD); \
	fi
	cd $(CURRENT_DIR)/$(SRC_DIR) && $(CONFIG_CMD); \
	$(MAKE) -C $(CURRENT_DIR)/$(SRC_DIR)
	$(MAKE) -C $(CURRENT_DIR)/$(SRC_DIR) install
	install -m 755 $(LOCAL_INSTALL_LIB_DIR)/lib/libipset.so* $(INSTALL_LIB_DIR)/lib
	install -m 755 $(LOCAL_INSTALL_LIB_DIR)/sbin/$(SBIN) $(INSTALL_LIB_DIR)/sbin

$(LIBXML2_LIB_PATH)/libtool.so:
	$(MAKE) -C $(LIBXML2_BUILD_PATH)
	
clean:
	$(MAKE) -C $(LIBXML2_BUILD_PATH) clean
	rm -rf $(LOCAL_INSTALL_LIB_DIR)
	rm -fr $(SRC_DIR)
	rm -rf $(INSTALL_LIB_DIR)/sbin/$(SBIN)
	rm -rf $(INSTALL_LIB_DIR)/lib/libipset.so*
