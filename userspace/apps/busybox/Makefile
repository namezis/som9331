PKG_NAME		:= busybox-1.23.0
PKG_SOURCE		:= $(PKG_NAME).tar.bz2
PKG_SOURCE_URL		:= http://busybox.net/downloads/$(PKG_SOURCE)
PKG_UNTAR		:= tar -jxvf

#export CC		= /opt/toolchains/OpenWrt-Toolchain-ar71xx-for-mips_34kc-gcc-4.8-linaro_uClibc-0.9.33.2/toolchain-mips_34kc_gcc-4.8-linaro_uClibc-0.9.33.2/bin/mips-openwrt-linux-gcc
#export CFLAGS		+= 
#export LDFLAGS		+= -L/opt/toolchains/OpenWrt-Toolchain-ar71xx-for-mips_34kc-gcc-4.8-linaro_uClibc-0.9.33.2/toolchain-mips_34kc_gcc-4.8-linaro_uClibc-0.9.33.2/lib
#export LIBS		+= -ldl

CUR_DIR			:= $(shell pwd)
PKG_CONFIG		=  cp $(CUR_DIR)/defconfig $(CUR_DIR)/$(PKG_NAME)/.config
MAKE_DIR		= $(CUR_DIR)/$(PKG_NAME)/

export 	Q		:= @

.PHONY: all install

check_untar_patch:
	$(Q)if [ ! -d $(CUR_DIR)/$(PKG_NAME) ]; then \
		if [ ! -f $(CUR_DIR)/$(PKG_SOURCE) ]; then \
			echo $(PKG_SOURCE) do not exist! Download from $(PKG_SOURCE_URL); \
			wget -P $(CUR_DIR) $(PKG_SOURCE_URL); \
		fi ;\
		$(PKG_UNTAR) $(PKG_SOURCE) 2> /dev/null ;\
		$(PKG_CONFIG);\
	fi

all: check_untar_patch
	cd $(MAKE_DIR); make; make install

clean:
	if [ -d $(MAKE_DIR) ]; then \
		cd $(MAKE_DIR); make clean; \
	fi;

install:
	cp -rf $(MAKE_DIR)/_install/* $(ROOTFS_DIR)/
	
