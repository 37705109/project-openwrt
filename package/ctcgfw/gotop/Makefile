include $(TOPDIR)/rules.mk

PKG_NAME:=gotop
PKG_VERSION:=4.0.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/xxxserxxx/gotop.git
PKG_MIRROR_HASH:=b4de9c3fdd144f57dfd713471c9ac7e99ff82b110e1dc0d7ecf1e3d0aaf5058d
PKG_SOURCE_VERSION:=a8a238ac18725e377addae8a23bf08cf476b404c
PKG_MAINTAINER:=[CTCGFW] Project OpenWrt

PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE:=$(PKG_SOURCE_SUBDIR).tar.gz
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_SOURCE_SUBDIR)

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/xxxserxxx/gotop
GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:= \
	main.Version=$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/$(PKG_NAME)
	SECTION:=admin
	CATEGORY:=Administration
	TITLE:=A terminal based graphical activity monitor
	URL:=https://github.com/xxxserxxx/gotop
	DEPENDS:=$(GO_ARCH_DEPENDS)
endef

define Package/$(PKG_NAME)/description
	Another terminal based graphical activity monitor,
	inspired by gtop and vtop, this time written in Go!
endef

define Build/Prepare
	tar -zxf $(DL_DIR)/$(PKG_SOURCE) -C $(PKG_BUILD_DIR) --strip-components 1
endef

define Build/Configure
endef

define Build/Compile
	$(eval GO_PKG_BUILD_PKG:=$(GO_PKG)/cmd/gotop)
	$(call GoPackage/Build/Configure)
	$(call GoPackage/Build/Compile)
	$(STAGING_DIR_HOST)/bin/upx --lzma --best $(GO_PKG_BUILD_BIN_DIR)/gotop
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/gotop $(1)/usr/bin/gotop
endef

$(eval $(call GoBinPackage,$(PKG_NAME)))
$(eval $(call BuildPackage,$(PKG_NAME)))
