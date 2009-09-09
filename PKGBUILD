# Maintainer:  Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=aircrack-ng
pkgver=1.0
pkgrel=2
pkgdesc="A key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=('i686' 'x86_64')
url="http://www.aircrack-ng.org"
license=('GPL2')
depends=('openssl' 'sqlite3' 'iw')
source=("http://download.aircrack-ng.org/${pkgname}-${pkgver}.tar.gz")
md5sums=('dafbfaf944ca9d523fde4bae86f0c067')
options=(force)

build() {
  cd ${srcdir}/${pkgname}-${pkgver}
  make SQLITE=true unstable=true || return 1
  make DESTDIR=${pkgdir} SQLITE=true unstable=true bindir=/usr/bin mandir=/usr/share/man/man1 sbindir=/usr/sbin install || return 1
}

# vim:set ts=2 sw=2 et:
