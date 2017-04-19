include env.rule

.PHONY: all clean 

all: libxml2 libnetconf-master clean

libxml2:
	$(MAKE) -C $(TOP_DIR)/libxml2

libnetconf-master:
	$(MAKE) -C $(TOP_DIR)/libnetconf
	
clean:
	rm -rf $(TOP_DIR)/libxml2/install
	rm -rf $(TOP_DIR)/libxml2/libxml2-master
