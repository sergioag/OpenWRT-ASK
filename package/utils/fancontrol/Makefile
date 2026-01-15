include $(TOPDIR)/rules.mk

PKG_NAME:=fancontrol
PKG_VERSION:=1.0
PKG_RELEASE:=1

PKG_MAINTAINER:=Tomaz Zaman <tomaz@mono.si>
PKG_LICENSE:=GPL-2.0-or-later

include $(INCLUDE_DIR)/package.mk

define Package/fancontrol
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Fan speed control for EMC2305
  DEPENDS:=
endef

define Package/fancontrol/description
  Simple fan control script for EMC2305 fan controller.
  Provides linear temperature-based PWM control without
  requiring pwm_enable support.
endef

define Build/Compile
endef

define Package/fancontrol/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) ./files/fancontrol-emc2305 $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/fancontrol.init $(1)/etc/init.d/fancontrol

	# Enable service by default
	$(INSTALL_DIR) $(1)/etc/rc.d
	ln -sf ../init.d/fancontrol $(1)/etc/rc.d/S99fancontrol
endef

$(eval $(call BuildPackage,fancontrol))
