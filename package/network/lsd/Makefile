include $(TOPDIR)/rules.mk

PKG_NAME:=lsd
PKG_RELEASE:=1

PKG_MAINTAINER:=Wambui Karuga <wambui@janga.la>
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_RELEASE)

include $(INCLUDE_DIR)/package.mk

TARGET_CFLAGS += \
	-I$(STAGING_DIR)/usr/include/libnl3 \
	-I$(STAGING_DIR)/usr/include

TARGET_LDFLAGS += -Wl,--gc-sections

MAKE_FLAGS += \
	CFLAGS="$(TARGET_CFLAGS)" \
	LDFLAGS="$(TARGET_LDFLAGS)"

define Package/lsd
	SECTION:=net
	CATEGORY:=JNG
	DEPENDS:=+libnl-tiny +libnl-genl
	TITLE:=Low Signal Disconnect
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) /home/wambui/jangala/lsd/* $(PKG_BUILD_DIR)/
endef

define Package/lsd/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/disconnect $(1)/usr/sbin/disconnect
endef

$(eval $(call BuildPackage,lsd))