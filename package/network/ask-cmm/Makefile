#
# Copyright (C) 2026 Mono Technologies Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ask-cmm
PKG_VERSION:=17.03.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/we-are-mono/ASK
PKG_SOURCE_VERSION:=master
PKG_SOURCE_SUBDIR:=$(PKG_NAME)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING.GPL

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1
PKG_BUILD_PARALLEL:=0

include $(INCLUDE_DIR)/package.mk

define Package/ask-cmm
  SECTION:=net
  CATEGORY:=Network
  TITLE:=NXP ASK Connection Manager daemon
  DEPENDS:=@TARGET_layerscape +libnetfilter-conntrack +libfci +libcli +libpcap \
	+kmod-ask-auto-bridge +kmod-nf-conntrack +kmod-nf-conntrack-netlink +kmod-nf-nat \
	+kmod-br-netfilter
  URL:=https://github.com/we-are-mono/ASK
endef

define Package/ask-cmm/description
  Connection Manager Module (CMM) daemon for managing fast path network
  offloading on NXP Layerscape processors. Part of the Application
  Solutions Kit (ASK).
endef

# The source is in cmm-X.XX.X subdirectory
define Build/Prepare
	$(call Build/Prepare/Default)
	$(CP) $(PKG_BUILD_DIR)/cmm/* $(PKG_BUILD_DIR)/
endef

# Build flags per NXP ASK documentation
TARGET_CFLAGS += \
	-Wno-error \
	-DLS1043 \
	-DFLOW_STATS \
	-DWIFI_ENABLE \
	-DSEC_PROFILE_SUPPORT \
	-DUSE_QOSCONNMARK \
	-DENABLE_INGRESS_QOS \
	-DIPSEC_NO_FLOW_CACHE \
	-DVLAN_FILTER \
	-DAUTO_BRIDGE

define Package/ask-cmm/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/cmm $(1)/usr/sbin/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libcmm.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/fastforward $(1)/etc/config/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/cmm.init $(1)/etc/init.d/cmm
endef

$(eval $(call BuildPackage,ask-cmm))
