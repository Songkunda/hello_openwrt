# hello_openwrt

openwrt feeds repo
## support
 
openwrt20+

## how 2 use

### add feed repo

```shell 
sed -i "/skd/d" "feeds.conf.default"
echo "src-git skd https://github.com/Songkunda/hello_openwrt.git" >> "feeds.conf.default"
```

### update this repo

```shell
./scripts/feeds update skd
./scripts/feeds install -a skd
```
### 

### remove this repo

```shell
sed -i "/skd/d" "feeds.conf.default"
./scripts/feeds clean
```

### i18n

```shell
./luci/build/i18n-scan.pl k3/luci-app-v2ray-client-client > k3/luci-app-v2ray-client/po/templates/v2ray-client.pot
./luci/build/i18n-update.pl k3/luci-app-v2ray-client/po

```

### dev
```shell 
#uci commit luci以禁用代码缓存以用于开发目的。
uci set luci.ccache.enable=0; 

```
