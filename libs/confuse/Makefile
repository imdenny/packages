#
# Copyright (C) 2006-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=confuse
PKG_VERSION:=3.0
PKG_RELEASE:=1

#PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
#PKG_SOURCE_URL:=http://savannah.nongnu.org/download/confuse/
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.xz
PKG_SOURCE_URL:=https://github.com/libconfuse/releases/download/v$(PKG_VERSION)/
PKG_MD5SUM:=c534b51a2118ed57031dc548032304a3
PKG_MAINTAINER:=Steven Barth <cyrus@openwrt.org>
PKG_LICENSE:=ISC

PKG_FIXUP:=autoreconf

include $(INCLUDE_DIR)/package.mk

define Package/confuse
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=libConfuse is a configuration file parser library
  URL:=http://www.nongnu.org/confuse/
endef

define Package/confuse/description
	libConfuse is a configuration file parser library, licensed under the
	terms of the ISC license, and written in C. It supports sections and
	(lists of) values (strings, integers, floats, booleans or other
	sections), as well as some other features (such as single/double-quoted
	strings, environment variable expansion, functions and nested include
	statements). It makes it very easy to add configuration file capability
	to a program using a simple API.

	The goal of libConfuse is not to be the configuration file parser
	library with a gazillion of features. Instead, it aims to be easy to use
	and quick to integrate with your code. libConfuse was called libcfg
	before, but was changed to not confuse with other similar libraries.
endef

TARGET_CFLAGS += $(FPIC)

CONFIGURE_ARGS += \
	--enable-shared \
	--enable-static \
	--disable-rpath \
	--without-libiconv-prefix \
	--without-libintl-prefix \

MAKE_FLAGS += \
	-C $(PKG_BUILD_DIR)/src \
	DESTDIR="$(PKG_INSTALL_DIR)" \
	all install \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/confuse.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libconfuse.{a,so*} $(1)/usr/lib/
	$(CP) $(PKG_BUILD_DIR)/*.pc $(1)/usr/lib/pkgconfig/
endef

define Build/UninstallDev
	rm -rf \
	$(STAGING_DIR)/usr/include/confuse.h \
	$(STAGING_DIR)/usr/lib/libconfuse.{a,so*}
endef

define Package/confuse/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libconfuse.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,confuse))
