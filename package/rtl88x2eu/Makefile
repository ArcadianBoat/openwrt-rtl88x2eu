include $(TOPDIR)/rules.mk
include $(INCLUDE_DIR)/kernel.mk
include $(INCLUDE_DIR)/package.mk

PKG_NAME:=rtl88x2eu
PKG_RELEASE:=1
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)

define KernelPackage/rtl88x2eu
  SUBMENU:=Wireless Drivers
  TITLE:=Realtek RTL8812EU/RTL8822EU USB WiFi driver
  DEPENDS:=+kmod-cfg80211
  FILES:=$(PKG_BUILD_DIR)/8812eu.ko
  AUTOLOAD:=$(call AutoProbe,8812eu)
endef

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	$(CP) $(CURDIR)/src/. $(PKG_BUILD_DIR)/
endef

define Build/Compile
	$(KERNEL_MAKE) M="$(PKG_BUILD_DIR)" \
		CONFIG_RTL8822E=y \
		CONFIG_RTL8822EU=m \
		CONFIG_USB_HCI=y \
		CONFIG_PLATFORM_ARM_RPI=y \
		USER_MODULE_NAME=8812eu \
		KCFLAGS="-Wno-error=missing-prototypes" \
		modules
endef

$(eval $(call KernelPackage,rtl88x2eu))
