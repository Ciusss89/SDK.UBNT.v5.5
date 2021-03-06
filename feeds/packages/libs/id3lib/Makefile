# 
# Copyright (C) 2006 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 12228 2008-08-06 22:43:15Z nbd $

include $(TOPDIR)/rules.mk

PKG_NAME:=id3lib
PKG_VERSION:=3.8.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=@SF/id3lib
PKG_MD5SUM:=19f27ddd2dda4b2d26a559a4f0f402a7

PKG_FIXUP = libtool

include $(INCLUDE_DIR)/package.mk

define Package/id3lib
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+zlib +uclibcxx
  TITLE:=An ID3v1/ID3v2 tag manipulation library
  URL:=http://www.id3lib.org/
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \

CONFIGURE_VARS += \
	CXXFLAGS="$$$$CXXFLAGS -fno-builtin -fno-rtti"  \
	LIBS="-nodefaultlibs -lz -luClibc++ -Wl,-Bstatic,-lstdc++,-Bdynamic -lm" \

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) DESTDIR="$(PKG_INSTALL_DIR)" all install
endef

define Build/InstallDev
	mkdir -p $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/id3 $(1)/usr/include/
	$(CP) $(PKG_INSTALL_DIR)/usr/include/id3.h $(1)/usr/include/
	mkdir -p $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libid3.{a,so} $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libid3-*.so.* $(1)/usr/lib/
endef

define Package/id3lib/install
	$(INSTALL_DIR) $(1)/usr/lib/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libid3-*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,id3lib))
