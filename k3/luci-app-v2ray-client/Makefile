include $(TOPDIR)/rules.mk

PKG_NAME:=luci-app-v2ray-client
PKG_VERSION:=1
PKG_RELEASE:=1
PKG_MAINTAINER:=Kunda.Song <574779754@qq.com>
PKG_DATE:=20220419

LUCI_TITLE:=V2ray Client LuCI interface by Kunda.Song
#限制平台
LUCI_PKGARCH:=all
#依赖
LUCI_DEPENDS:=+v2ray-core

# 设置config file 文件目录
define Package/$(PKG_NAME)/conffiles
/etc/config/v2ray
endef

#加载规则文件 *
include $(TOPDIR)/feeds/luci/luci.mk


# 下面一行是 Luci 界面专用调用标识，必需，如果缺失会导致不会被加入 OpenWrt 的编译菜单中。
# call BuildPackage - OpenWrt buildroot signature
