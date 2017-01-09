#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=obfs4proxy
PKG_VERSION:=0.0.1
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=https://github.com/Yawning/obfs4.git
PKG_SOURCE_VERSION:=97a875ec3c0afa629405c78e750d27e4e1f851ca
PKG_SOURCE:=$(PKG_NAME)-$(PKG_SOURCE_VERSION).tar.gz
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

PKG_MAINTAINER:=<x.paja@email.cz>
PKG_LICENSE:=GPL-3.0

include $(INCLUDE_DIR)/package.mk

define Package/obfs4proxy
	SECTION:=net
	CATEGORY:=Network
	SUBMENU:=IP Addresses and Names
	TITLE:=obfs4proxy
endef

define Package/$(PKG_NAME)/description
  Pluggable Transports (PT) transform the Tor traffic flow between the client and the bridge.
endef

OBFS_DIR:=$(PKG_BUILD_DIR)/obfs4proxy/
ENV_CMD=export GOPATH=$(OBFS_DIR) && export GOARCH=arm && export GOARM=7

define Build/Compile
	mkdir $(OBFS_DIR)bin
	$(ENV_CMD) && export GOBIN=$(OBFS_DIR)bin/  && cd $(OBFS_DIR) && go env && go get -d .
	$(ENV_CMD) && export GOBIN=$(OBFS_DIR)bin/  && cd $(OBFS_DIR) && go env && go build .
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin/
	$(CP) $(OBFS_DIR)obfs4proxy $(1)/usr/bin/obfs4proxy
endef

$(eval $(call BuildPackage,obfs4proxy))

