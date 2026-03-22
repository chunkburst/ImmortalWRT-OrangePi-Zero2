# ImmortalWrt For Orange Pi Zero 2 (WIFI)

  

由于香橙派官方OpenWRT镜像都没有无线驱动（完全不认）。且互联网中很少有完整的 Zero 2 的带WIFI固件，于是自己搓了一个


[Release - 固件下载](https://github.com/chunkburst/ImmortalWRT-OrangePi-Zero2/releases)


### ✅ 适配信息

- **Board**: Orange Pi Zero 2 (H616)
- **Wi-Fi Chip**: UWE5622
- **OS Base**: ImmortalWrt 24.10



>  ⚠️ 注：因为蓝牙的 `tty-sdio / sprdbt_tty` 会导致莫名其妙编译错误，因此这个固件为 WI-FI Only 方案（感兴趣的大佬可以自己改下） 



![Zero2](https://pic1.imgdb.cn/item/69bee3264235741b1e4389d9.png)



### 📦 自带模块：

- `kmod-uwe5622`

- `uwe5622-firmware`
- `wpad-basic-mbedtls`



> ❗ 此源码&固件仅适用于 Orange Pi Zero 2，其他型号请使用其他固件



---



![Zero2](https://pic1.imgdb.cn/item/69bee2e84235741b1e4389d7.png)



![Zero2](https://pic1.imgdb.cn/item/69bee3474235741b1e4389db.png)





## 🚀 快速开始



### 1. 拉源码

```bash
git clone https://github.com/chunkburst/ImmortalWRT-OrangePi-Zero2
cd ImmortalWRT-OrangePi-Zero2
```



### 2. 更新 feeds

```bash
./scripts/feeds update -a
./scripts/feeds install -a
```



### 3. 生成默认配置

```bash
make defconfig
```



### 4. 开始编译

```bash
make -j$(nproc) V=s
```

💡 如果编译出错了可以使用单线程(方便查看日志)

```bash
make -j1 V=s
```

会慢一点，但至少日志干净很多。



---



## 🛠 编译环境

建议使用 Ubuntu / Debian。  

我的环境是： Debian 12

- 4GB 以上内存
- 25GB 以上可用空间
- 尽量不要在奇怪的中文路径或带空格路径里编



### Ubuntu / Debian 依赖

```bash
sudo apt update -y
sudo apt full-upgrade -y
sudo apt install -y ack antlr3 asciidoc autoconf automake autopoint binutils bison build-essential \
  bzip2 ccache clang cmake cpio curl device-tree-compiler ecj fastjar flex gawk gettext gcc-multilib \
  g++-multilib git gnutls-dev gperf haveged help2man intltool lib32gcc-s1 libc6-dev-i386 libelf-dev \
  libglib2.0-dev libgmp3-dev libltdl-dev libmpc-dev libmpfr-dev libncurses-dev libpython3-dev \
  libreadline-dev libssl-dev libtool libyaml-dev libz-dev lld llvm lrzsz mkisofs msmtp nano \
  ninja-build p7zip p7zip-full patch pkgconf python3 python3-pip python3-ply python3-docutils \
  python3-pyelftools qemu-utils re2c rsync scons squashfs-tools subversion swig texinfo uglifyjs \
  upx-ucl unzip vim wget xmlto xxd zlib1g-dev zstd
```

---



## 🎯 默认编译目标

这份源码默认面向：

- `Target System`: `Allwinner ARM Socs `
- `Subtarget`: `AllWinner A64/H5/H6/H616/H618`
- `Target Profile`: `Xunlong Orange Pi Zero 2`

想自己确认的话：

```bash
make menuconfig
```

---



## 📁 编译完成后固件位置

一般在这里：

```bash
bin/targets/sunxi/cortexa53
```

常见输出：

- `immortalwrt-sunxi-cortexa53-xunlong_orangepi-zero2-ext4-sdcard.img.gz`
- `immortalwrt-sunxi-cortexa53-xunlong_orangepi-zero2-squashfs-sdcard.img.gz`



---



## ✅ 确认成功编译WIFI模块



### manifest

```bash
grep -E 'kmod-uwe5622|wpad-basic-mbedtls' bin/targets/sunxi/cortexa53/*.manifest
```



示例输出

```bash
root@MAIN:~/immortalwrt# grep -E 'kmod-uwe5622|wpad-basic-mbedtls' bin/targets/sunxi/cortexa53/*.manifest
kmod-uwe5622 - 6.6.127.6.12.61-r1
wpad-basic-mbedtls - 2024.09.15~5ace39b0-r2
root@MAIN:~/immortalwrt# 
```



### 内核模块

如果构建成功，通常能在 build 目录里看到：

- `sprdwl_ng.ko`
- `uwe5622_bsp_sdio.ko`



### 镜像固件

最终镜像里的 `/lib/firmware` 应该至少有：

- `wcnmodem.bin`
- `wcnmodem-38222.bin`
- `wifi_2355b001_1ant.ini`



## 🙏 致谢

- ImmortalWrt
- OpenWrt
- DeepAQ -  `openwrt-uwe5622-sunxi`
- Armbian firmware



---



## 📄 License

[MIT](https://github.com/chunkburst/ImmortalWRT-OrangePi-Zero2/blob/main/LICENSE)
