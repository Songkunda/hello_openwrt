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

./build/i18n-scan.pl k3/luci-app-v2ray-client-client > k3/luci-app-v2ray-client/po/templates/v2ray-client.pot
./build/i18n-update.pl k3/luci-app-v2ray-client/po

```

### dev

```shell
 
#uci commit luci以禁用代码缓存以用于开发目的。
uci set luci.ccache.enable=0; 

```


### makefile 变量

* ''PKG_NAME''        - 包的名称，可以通过menuconfig和ipkg看到。避免在包名称中使用下划线，以避免构建失败——例如，下划线将名称与版本信息分隔开，这可能会在难以识别的地方混淆构建系统。
* ''PKG_VERSION''     - 我们正在下载的上游版本号
* ''PKG_RELEASE''     - Makefile包的版本
* ''PKG_LICENSE''     - 软件包的许可证形式为 [SPDX](https://spdx.org/licenses/) 。
* ''PKG_LICENSE_FILES''- 包含许可证文本的文件
* ''PKG_BUILD_DIR''   - 编译包目录
* ''PKG_SOURCE''      - 原始源的文件名
* ''PKG_SOURCE_URL''  - 从哪里下载源码(目录)
* ''PKG_HASH''        - 验证下载的校验和。可以是MD5校验和，也可以是SHA256校验和，但应该使用SHA256 ,参考 [scripts/download.pl](https://git.lede-project.org/?p=source.git;a=blob;f=scripts/download.pl;h=90d50a88622f26f554344f20b07f9da7ba649e74;hb=HEAD#l63)
* ''PKG_CAT''         - 如何解压源文件(zcat, bzcat, unzip)
* ''PKG_BUILD_DEPENDS'' - 需要在此包之前构建的包。如果您需要确保您的包在构建时具有对另一个包的包含和/或库的访问权限，请使用此选项。指定目录名(即openssl)而不是二进制包名(即libopenssl)。此构建变量仅建立构建时依赖关系。使用“DEPENDS”来建立运行时依赖关系。此变量使用与下面的“DEPENDS”相同的语法。
* ''PKG_CONFIG_DEPENDS'' - 指定哪些配置选项影响生成配置，并应在更改时触发重新运行Build/Configure
* ''PKG_INSTALL''     - 将它设置为“1”将调用包的原始“make install”，前置设置 “PKG_INSTALL_DIR”
* ''PKG_INSTALL_DIR'' - “make install”复制编译文件目录
* 
* ''PKG_FIXUP''       - See below

Optional support for fetching sources from a VCS (git, bzr, svn, etc), see [使用源代码库](#use_source_repository) below for more information:

* ''PKG_SOURCE_PROTO'' - the protocol to use for fetching the sources (git, svn, etc).
* ''PKG_SOURCE_URL''  - source repository to fetch from.  The URL scheme must be consistent with ''PKG_SOURCE_PROTO'' (e.g. ''git:%%//%%''), but most VCS accept ''http:%%//%%'' or ''https:%%//%%'' URLs nowadays.
* ''PKG_SOURCE_VERSION'' - must be specified, the commit hash or SVN revision to check out.
* ''PKG_SOURCE_DATE'' - a date like ''2017-12-25'', will be used in the name of generated tarballs.
* ''PKG_MIRROR_HASH'' - SHA256 checksum of the tarball generated from the source repository checkout (previously named ''PKG_MIRROR_MD5SUM'').  See [#use_source_repository](below) for details.
* ''PKG_SOURCE_SUBDIR'' - where the temporary source checkout should be stored, defaults to ''$(PKG_NAME)-$(PKG_VERSION)''

The ''PKG_*'' variables define where to download the package from; @SF is a special keyword for downloading packages from sourceforge. The md5sum is used to verify the package was downloaded correctly and PKG_BUILD_DIR defines where to find the package after the sources are uncompressed into $(BUILD_DIR). PKG_INSTALL_DIR defines where the files will be copied after calling "make install" (set with the PKG_INSTALL variable), and after that you can package them in the install section.

At the bottom of the file is where the real magic happens, "BuildPackage" is a macro setup by the earlier include statements. BuildPackage only takes one argument directly -- the name of the package to be built, in this case "bridge". All other information is taken from the define blocks. This is a way of providing a level of verbosity, it's inherently clear what the DESCRIPTION variable in Package/bridge is, which wouldn't be the case if we passed this information directly as the Nth argument to BuildPackage.

Avoid reuse of PKG_NAME in call, define and eval lines for consistency and readability. Write the full name instead.


### 参考
- [pageages常量](https://openwrt.org/docs/guide-developer/packages)
