include $(TOP_DIR)/build/env.rule
APP = libxml2-master
CURRENT_DIR = $(shell pwd)
LOCAL_INSTALL_DIR = $(CURRENT_DIR)/install
CROSS_HOST = $(HOST) 

CFLAGS+=-DHAVE_NETINET_IN_H

CONFIG_CMD = $(CURRENT_DIR)/$(APP)/autogen.sh --prefix=$(LOCAL_INSTALL_DIR) --host=$(CROSS_HOST) --enable-static  PKG_CONFIG_PATH=$(WINDRIVER_BASE)/gnu/4.1.2-vxworks-6.6/x86-linux2/powerpc-wrs-vxworks/bin/ CC=$(CC) 
#--oldincludedir=$(C_INCLUDE_PATH)/wrn/coreip/ 

all:
	@if [ ! -d $(APP) ]; then \
	    echo "Untarring original $(APP) source"; \
	    (unzip $(APP).zip 2> /dev/null || true); \
	    mkdir -p $(LOCAL_INSTALL_DIR); \
	    cd $(CURRENT_DIR)/$(APP) && sh $(CONFIG_CMD); \
	fi
	@echo "CFLAGS=$(CFLAGS)"
	$(MAKE) -C $(CURRENT_DIR)/$(APP)
	$(MAKE) -C $(CURRENT_DIR)/$(APP) install
	install -m 755 $(LOCAL_INSTALL_DIR)/lib/libmnl.so* $(INSTALL_LIB_DIR)/

clean:
	rm -rf $(LOCAL_INSTALL_DIR)
	rm -fr $(APP)
	rm -rf $(INSTALL_LIB_DIR)/libmnl.so*

