# Maintainer: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=aircrack-ng
_pkgver=1.2-rc4
pkgver=${_pkgver//-/}
pkgrel=4
pkgdesc="Key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=('x86_64')
url="https://www.aircrack-ng.org"
license=('GPL2')
depends=('openssl' 'sqlite' 'iw' 'net-tools' 'wireless_tools' 'ethtool')
conflicts=('aircrack-ng-scripts')
replaces=('aircrack-ng-scripts')
provides=('aircrack-ng-scripts')
source=(https://download.aircrack-ng.org/$pkgname-$_pkgver.tar.gz
        9a1846507ff043c397257206ff21adae90a122f4.patch)
md5sums=('3bbc7d5035a98ec01e78774d05c3fcce'
         'efeab8202444d183b2fc02f455c1c294')

prepare() {
  cd $pkgname-$_pkgver

  patch -Np1 -i "$srcdir"/9a1846507ff043c397257206ff21adae90a122f4.patch
}

build() {
  cd $pkgname-$_pkgver

  make sqlite=true experimental=true
}

package() {
  cd $pkgname-$_pkgver

  make DESTDIR="$pkgdir" sqlite=true experimental=true \
    bindir=/usr/bin sbindir=/usr/bin mandir=/usr/share/man/man1/ \
    smandir=/usr/share/man/man8/ install
}
