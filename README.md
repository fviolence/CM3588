# Small HOWTO start fast Rockchip GPU based on [Jellyfin guide](https://jellyfin.org/docs/general/administration/hardware-acceleration/rockchip)

## Install all essential tools
```
sudo apt-get update
sudo apt-get install -y build-essential cmake git libdrm-dev dh-exec dpkg-dev debhelper clinfo wget
sudo apt-get clean
mkdir WD && cd WD
```

## Clone the MPP repository and build Debian packages
```
git clone https://github.com/rockchip-linux/mpp.git && cd mpp
DEB_BUILD_OPTIONS="parallel=$(nproc) nocheck" dpkg-buildpackage -b -us -uc -aarm64
```

## Install MPP and mali driver
```
cd ..
wget https://github.com/tsukumijima/libmali-rockchip/releases/download/v1.9-1-55611b0/libmali-valhall-g610-g13p0-gbm_1.9-1_arm64.deb
dpkg -i *.deb
ldconfig
```

## Check the OpenCL (GPU firmware)
```
clinfo
```
