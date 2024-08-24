
_pkgname=amneziawg
pkgname=${_pkgname}-dkms-git
pkgver=1.0.20220627.r7.gc981738
pkgrel=1
pkgdesc="AmnesiaWG kernel module"
arch=('any')
url="https://github.com/amnezia-vpn/amneziawg-linux-kernel-module"
license=('GPL2')
depends=('dkms')
makedepends=('git' 'wget')
provides=("${_pkgname}-dkms")
source=("git+${url}.git")
md5sums=('SKIP')

pkgver() {
    cd "amneziawg-linux-kernel-module"
    git describe --long --tags | sed 's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

check() {
    # Warning if missing linux-headers for current `uname -r` kernel
    if [ ! -f "/usr/lib/modules/$(uname -r)/build/Makefile" ]
    then
        _BOLDRED='\033[1;31m'
        _RED='\033[0;31m'
        _RESET='\033[0m'
        echo -e "${_BOLDRED}WARNING:${_RED} You may be missing headers for your current kernel, DKMS packages requires them."
        echo -e "Please refer to https://wiki.archlinux.org/title/Dynamic_Kernel_Module_Support for details.${_RESET}"
    fi
}

build() {
    cd "amneziawg-linux-kernel-module/src"

    kernel_major=$(uname -r | cut -d '.' -f 1)
    kernel_ver=$(uname -r | sed 's/[-].*//' | cut -d '.' -f 1,2,3)

    if [ -r "kernel" ];
    then
        rm kernel
    fi

    if [ ! -d "linux-${kernel_ver}" ]; then
        wget "https://cdn.kernel.org/pub/linux/kernel/v${kernel_major}.x/linux-${kernel_ver}.tar.xz";
        unxz linux-${kernel_ver}.tar.xz 
        tar -xf linux-${kernel_ver}.tar
        # TODO: Check signature
    fi

    ln -s "linux-${kernel_ver}" kernel

    make
}

package() {
    cd "amneziawg-linux-kernel-module/src"

    DEPMOD="true" make module-install INSTALL_MOD_PATH="$pkgdir/usr"
}
