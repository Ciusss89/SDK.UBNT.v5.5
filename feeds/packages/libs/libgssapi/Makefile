# 
# Copyright (C) 2007 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 12228 2008-08-06 22:43:15Z nbd $

include $(TOPDIR)/rules.mk

PKG_NAME:=libgssapi
PKG_VERSION:=0.11
PKG_RELEASE:=2

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://www.citi.umich.edu/projects/nfsv4/linux/libgssapi/
PKG_MD5SUM:=0e5b4c7267724f8ddf64bc35514c272e

include $(INCLUDE_DIR)/package.mk

define Package/libgssapi
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=required libraries for the nfs-utils
  URL:=http://www.citi.umich.edu/projects/nfsv4/linux
endef

define Package/libgssapi/description
 Support libraries - for newer nfs mount command (nfs4)
endef

TARGET_CFLAGS += -I$(PKG_BUILD_DIR)/lib $(FPIC)

MAKE_FLAGS += \
	OPT="$(TARGET_CFLAGS)" \
	INSTALLSUID="install -m 4755" \
	DESTDIR="$(PKG_INSTALL_DIR)" \
	all install

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include/gssglue/gssapi
	$(CP) $(PKG_INSTALL_DIR)/usr/include/gssglue/gssapi/gssapi.h $(1)/usr/include/gssglue/gssapi
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libgssapi.{a,so*} $(1)/usr/lib
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/libgssapi.pc $(1)/usr/lib/pkgconfig
endef

$(eval $(call BuildPackage,libgssapi))
