# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=wizfi630s_package
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/wizfi630s_package
  TITLE:=WizFi630S support package
  DEPENDS:=@TARGET_ramips_mt76x8_DEVICE_wizfi630s \
  	+curl +strace +coreutils +coreutils-stty \
	+uhttpd +uhttpd-mod-ubus +rpcd +rpcd-mod-iwinfo \
	+luci +luci-theme-openwrt +luci-lib-json\
	+rpcd-mod-rpcsys +cgi-io +uboot-envtools
  SECTION:=WIZnet Properties
  CATEGORY:=WIZnet Properties
  SUBTITLE:=Default package
  DEFAULT:=y
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
endef

define Build/Compile
	$(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/pinmux src/pinmux.c ; \
	$(TARGET_CC) $(TARGET_CFLAGS) $(EXTRA_CFLAGS) -Wall -Werror -o $(PKG_BUILD_DIR)/refclk src/refclk.c
endef

define Package/wizfi630s_package/install
	$(INSTALL_DIR) $(1)/sbin
	
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/pinmux $(1)/sbin/pinmux
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/refclk $(1)/sbin/reclk
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,wizfi630s_package))
