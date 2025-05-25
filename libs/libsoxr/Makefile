#
# Copyright (C) 2014 OpenWrt.org  
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
# updated to work with latest source from abrasive
#

include $(TOPDIR)/rules.mk

PKG_NAME:=soxr
PKG_VERSION:=0.1.2
PKG_RELEASE:=2

PKG_SOURCE:=soxr-$(PKG_VERSION)-Source.tar.xz
PKG_SOURCE_URL:=https://sourceforge.net/projects/soxr/files/
PKG_HASH:=b111233d55dac0d064a2ee5eb6c4d5c64c68317955

PKG_BUILD_DIR := $(BUILD_DIR)/soxr-$(PKG_VERSION)-Source


PKG_LICENSE:=LGPL-2.1
PKG_LICENSE_FILES:=LICENCE

PKG_FIXUP:=libtool
PKG_REMOVE_FILES:=autogen.sh


PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk


define Package/libsoxr
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=The SoX Resampler library
  URL:=http://sourceforge.net/projects/soxr/
  MAINTAINER:=Mike Brady <mikebrady@eircom.net>
  DEPENDS:= +libpthread
endef

define Package/libsoxr/description
  The SoX Resampler library
  High quality, one-dimensional sample-rate conversion library
endef

CMAKE_OPTIONS:= -DBUILD_SHARED_LIBS=OFF -DBUILD_TESTS=0 -DBUILD_EXAMPLES=0
CMAKE_OPTIONS+= -DHAVE_WORDS_BIGENDIAN_EXITCODE=$(if $(CONFIG_BIG_ENDIAN),0,1)


#CONFIGURE_ARGS += --disable-shared --disable-examples --disable-tests


define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/src/soxr.h $(1)/usr/include/
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/*.a $(1)/usr/lib/
	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/pkgconfig/*.pc $(1)/usr/lib/pkgconfig/
endef

define Package/libsoxr/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_BUILD_DIR)/src/*.a $(1)/usr/lib/
endef


$(eval $(call BuildPackage,libsoxr))
