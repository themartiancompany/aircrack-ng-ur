# Maintainer: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgname=aircrack-ng
pkgver=1.0_rc3
pkgrel=1
pkgdesc="A key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=('i686' 'x86_64')
url="http://www.aircrack-ng.org"
license=('GPL2')
depends=('openssl' 'sqlite3')
source=("http://download.aircrack-ng.org/${pkgname}-${pkgver/_/-}.tar.gz")
md5sums=('37884de939af82eab60d3e7d165b40ad')

build() {
  cd ${srcdir}/${pkgname}-${pkgver/_/-}
  make SQLITE=true || return 1
  make DESTDIR=${pkgdir} SQLITE=true bindir=/usr/bin mandir=/usr/share/man/man1 sbindir=/usr/sbin install || return 1
}

# vim:set ts=2 sw=2 et:
