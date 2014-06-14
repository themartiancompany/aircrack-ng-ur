# Maintainer: Jonathan Steel <jsteel at aur.archlinux.org>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=aircrack-ng
_pkgver=1.2-beta3
pkgver=${_pkgver//-/}
pkgrel=1
pkgdesc="A key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=('i686' 'x86_64')
url="http://www.aircrack-ng.org"
license=('GPL2')
depends=('openssl' 'sqlite' 'iw' 'net-tools' 'wireless_tools')
conflicts=('aircrack-ng-scripts')
replaces=('aircrack-ng-scripts')
provides=('aircrack-ng-scripts')
source=(http://download.aircrack-ng.org/$pkgname-$_pkgver.tar.gz)
md5sums=('ec5492e65ce7e98c6812e84b1d18d811')

build() {
  cd "$srcdir"/$pkgname-$_pkgver

  make sqlite=true unstable=true
}

package() {
  cd "$srcdir"/$pkgname-$_pkgver

  make DESTDIR="$pkgdir" sqlite=true unstable=true \
    bindir=/usr/bin sbindir=/usr/bin mandir=/usr/share/man/man1/ \
    smandir=/usr/share/man/man8/ install
}
