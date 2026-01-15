#
# Copyright (C) 2026 Mono Technologies Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk

PKG_NAME:=ask-auto-bridge
PKG_VERSION:=6.02.0
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/we-are-mono/ASK
PKG_SOURCE_VERSION:=mono-patched
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(KERNEL_BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_LICENSE:=GPL-2.0-or-later
PKG_LICENSE_FILES:=COPYING.GPL

include $(INCLUDE_DIR)/package.mk

define KernelPackage/ask-auto-bridge
  SUBMENU:=Network Devices
  TITLE:=NXP ASK automatic bridge module
  DEPENDS:=@TARGET_layerscape
  FILES:=$(PKG_BUILD_DIR)/auto_bridge-$(PKG_VERSION)/auto_bridge.ko
  AUTOLOAD:=$(call AutoProbe,auto_bridge)
endef

define KernelPackage/ask-auto-bridge/description
  Automatic bridge management kernel module for fast path offloading.
  Part of the NXP Application Solutions Kit (ASK).
endef

# Build in the auto_bridge subdirectory
BRIDGE_DIR:=$(PKG_BUILD_DIR)/auto_bridge-$(PKG_VERSION)

define Build/Compile
	$(KERNEL_MAKE) \
		M="$(BRIDGE_DIR)" \
		PLATFORM=LS1043A \
		ENABLE_VLAN_FILTER=y \
		KERNEL_SRC="$(LINUX_DIR)" \
		modules
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(BRIDGE_DIR)/include/auto_bridge.h $(1)/usr/include/
endef

$(eval $(call KernelPackage,ask-auto-bridge))
