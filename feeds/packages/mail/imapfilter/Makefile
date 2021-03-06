# 
# Copyright (C) 2006-2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# $Id: Makefile 12726 2008-09-27 11:25:41Z nbd $

include $(TOPDIR)/rules.mk

PKG_NAME:=imapfilter
PKG_VERSION:=2.0.10
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://imapfilter.hellug.gr/source/
PKG_MD5SUM:=7a82c69a71105da185cb4dd7c57b01f7

include $(INCLUDE_DIR)/package.mk

define Package/imapfilter
  SECTION:=mail
  CATEGORY:=Mail
  DEPENDS:=+liblua +libopenssl +libpcre
  TITLE:=IMAP server based email filtering
  URL:=http://imapfilter.hellug.gr/
endef

define Package/imapfilter/description
	IMAPFilter is a mail filtering utility. It connects to remote mail
	servers using the Internet Message Access Protocol (IMAP), sends
	searching queries to the server and processes mailboxes based on the
	results. It can be used to delete, copy, move, flag, etc. messages
	residing in mailboxes at the same or different mail servers. The 4rev1
	and 4 versions of the IMAP protocol are supported.

	IMAPFilter uses the Lua programming language as a configuration and
	extension language.
endef

define Build/Configure
	(cd $(PKG_BUILD_DIR); \
		./configure \
			-d /usr \
	);
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		INCDIRS="-I$(STAGING_DIR)/usr/include -I$(STAGING_DIR)/include" \
		LIBDIRS="-L$(STAGING_DIR)/usr/lib -L$(STAGING_DIR)/lib" \
		MYCFLAGS="$(TARGET_CFLAGS)" \
		MYLDFLAGS="-lcrypt" 
endef

define Package/imapfilter/conffiles
/etc/imapfilter/config.lua
endef

define Package/imapfilter/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/imapfilter $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/imapfilter
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/sample.config.lua $(1)/etc/imapfilter/config.lua
	$(INSTALL_DIR) $(1)/usr/share/imapfilter
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/{account,auxiliary,common,mailbox,message,options,regex,set}.lua $(1)/usr/share/imapfilter/
endef

$(eval $(call BuildPackage,imapfilter))
