# Maintainer: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=aircrack-ng
_pkgver=1.2-rc5
pkgver=${_pkgver//-/}
pkgrel=2
pkgdesc="Key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=('x86_64')
url="https://www.aircrack-ng.org"
license=('GPL2')
depends=('openssl' 'sqlite' 'iw' 'net-tools' 'wireless_tools' 'ethtool')
conflicts=('aircrack-ng-scripts')
replaces=('aircrack-ng-scripts')
provides=('aircrack-ng-scripts')
source=(https://download.aircrack-ng.org/$pkgname-$_pkgver.tar.gz)
md5sums=('413f5b5483aabe8ca64030efa9355a92')

build() {
  cd $pkgname-$_pkgver

  ./autogen.sh

  ./configure --prefix=/usr

  make sqlite=true experimental=true
}

package() {
  cd $pkgname-$_pkgver

  make DESTDIR="$pkgdir" sqlite=true experimental=true \
    bindir=/usr/bin sbindir=/usr/bin mandir=/usr/share/man/man1/ \
    smandir=/usr/share/man/man8/ install
}
