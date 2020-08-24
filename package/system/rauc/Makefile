include $(TOPDIR)/rules.mk

PKG_NAME:=rauc
PKG_VERSION:=v1.4
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git@github.com:rauc/rauc.git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_VERSION:=ae9cee9f29fc3ba101c887cafe0bca89e4fadd80

PKG_MAINTAINER:=Enrico Jorns <e.joerns@pengutronix.de>

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
#PKG_BUILD_DEPENDS:=
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk

define Package/rauc
	SECTION:=core
	CATEGORY:=JNG
	TITLE:=Robust Auto-Update Controller
	DEPENDS:=+glib2 \
		+dbus
endef

define Package/rauc/description
RAUC controls the update process on embedded Linux systems.
It is both a target application that runs as an update client and a host/target tool that allows you to create, inspect and modify installation artifacts.
endef


define Build/Configure
	( cd $(PKG_BUILD_DIR); ./autogen.sh )
	$(call Build/Configure/Default)
endef

define Build/Compile
endef

define Package/rauc/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_DIR) $(1)/etc/dbus-1/system.d
	$(INSTALL_DIR) $(1)/usr/share/dbus-1/system-services

	$(INSTALL_BIN) $(PKG_BUILD_DIR)/rauc $(1)/usr/bin/rauc
	$(INSTALL_CONF) $(PKG_BUILD_DIR)/data/de.pengutronix.rauc.conf $(1)/etc/dbus-1/system.d
	$(INSTALL_DATA) $(PKG_BUILD_DIR)/data/de.pengutronix.rauc.service $(1)/usr/share/dbus-1/system-services
endef

define Package/rauc/postinst
	#!/bin/sh
	[ -n "$${IPKG_INST_ROOT}" ] && exit 0
	exit 0
endef

$(eval $(call BuildPackage,rauc))
