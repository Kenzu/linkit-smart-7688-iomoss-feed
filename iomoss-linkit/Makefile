# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.

include $(TOPDIR)/rules.mk

PKG_NAME:=iomoss-linkit
PKG_RELEASE:=1

include $(INCLUDE_DIR)/package.mk

define Package/iomoss-linkit
	TITLE:=iomoss LinkIt Smart board support package
	DEPENDS:=@TARGET_ramips_mt76x8_DEVICE_LinkIt7688 \
		+kmod-fs-ext4 +kmod-fs-vfat
	DEFAULT:=n
endef

define Build/Configure
	true
endef

define Build/Compile
	true
endef

define Package/iomoss-linkit/install
	$(CP) ./files/* $(1)
endef

$(eval $(call BuildPackage,iomoss-linkit))
