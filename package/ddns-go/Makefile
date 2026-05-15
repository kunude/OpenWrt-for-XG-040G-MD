include $(TOPDIR)/rules.mk

PKG_NAME:=ddns-go
PKG_VERSION:=master
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/jeessy2/ddns-go.git
PKG_SOURCE_VERSION:=master
PKG_MIRROR_HASH:=skip

PKG_LICENSE:=MIT
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=You <your@email.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/jeessy2/ddns-go
GO_PKG_LDFLAGS:=-X main.version=$(shell git -C $(PKG_BUILD_DIR) describe --tags --always 2>/dev/null || echo master) -X 'main.buildTime=$(shell date -u +"%Y-%m-%dT%H:%M:%SZ")'

include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/ddns-go
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=IP Addresses and Names
  TITLE:=Dynamic DNS client with web UI
  URL:=https://github.com/jeessy2/ddns-go
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle
endef

define Package/ddns-go/description
  Simple and easy to use DDNS. Support webhook, DNSPod, Alidns, Cloudflare, etc.
endef

define Build/Compile
	$(call GoPackage/Build/Compile)
endef

define Package/ddns-go/install
	$(call GoPackage/Build/Install)
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(GO_PKG_BUILD_BIN_DIR)/ddns-go $(1)/usr/bin/
endef

$(eval $(call GoBinPackage,ddns-go))
