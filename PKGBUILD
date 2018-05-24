# Maintainer: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=aircrack-ng
_pkgver=1.2
pkgver=${_pkgver//-/}
pkgrel=4
pkgdesc="Key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=('x86_64')
url="https://www.aircrack-ng.org"
license=('GPL2')
depends=('openssl' 'sqlite' 'iw' 'net-tools' 'wireless_tools' 'ethtool'
         'pcre' 'libpcap' 'python')
conflicts=('aircrack-ng-scripts')
replaces=('aircrack-ng-scripts')
provides=('aircrack-ng-scripts')
source=(https://download.aircrack-ng.org/$pkgname-$_pkgver.tar.gz)
md5sums=('bb11ec14e1fe505d8d0d51cee0c54df9')

build() {
  cd $pkgname-$_pkgver

  ./autogen.sh

  ./configure --prefix=/usr --libexecdir=/usr/lib

  make
}

check() {
  cd $pkgname-$_pkgver

  make check
}

package() {
  cd $pkgname-$_pkgver

  make DESTDIR="$pkgdir" pkglibexecdir=/usr/lib/aircrack-ng \
    sbindir=/usr/bin install
}
