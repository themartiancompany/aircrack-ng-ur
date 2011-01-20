# Maintainer: Brad Fanella <bradfanella@archlinux.us>
# Contributor:  Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgbase=aircrack-ng
pkgname=(aircrack-ng aircrack-ng-scripts)
pkgver=1.1
pkgrel=2
arch=('i686' 'x86_64')
url="http://www.aircrack-ng.org"
license=('GPL2')
source=("http://download.aircrack-ng.org/${pkgname}-${pkgver}.tar.gz")
md5sums=('f7a24ed8fad122c4187d06bfd6f998b4')
depends=('openssl' 'sqlite3' 'iw')

build() {
  	cd ${srcdir}/${pkgbase}-${pkgver}
  	make SQLITE=true unstable=true

}

package_aircrack-ng() {
	pkgdesc="A key cracker for the 802.11 WEP and WPA-PSK protocols"

  	cd ${srcdir}/${pkgname}-${pkgver}
	make DESTDIR=${pkgdir} SQLITE=true unstable=true bindir=/usr/bin  \
		mandir=/usr/share/man/man1 sbindir=/usr/sbin install
}

package_aircrack-ng-scripts() {
	pkgdesc="Included scripts for a key cracker for the 802.11 WEP and WPA-PSK protocols"
        depends=('python2')	

	cd ${srcdir}/${pkgname}-${pkgver}/scripts
	mkdir -p ${pkgdir}/usr/bin ${pkgdir}/usr/lib/python2.7/site-packages/
	
	# airdriver-ng
	install -Dm644 airdriver-ng ${pkgdir}/usr/bin/

	# airdrop-ng libs
	install -Dm644 airdrop-ng/lib/{colorize.py,libDumpParse.py,libOuiParse.py} \
		${pkgdir}/usr/lib/python2.7/site-packages/
	
	# airdrop-ng
	sed s/python/python2/ -i airdrop-ng/airdrop-ng.py
	install -Dm644 airdrop-ng/airdrop-ng.py ${pkgdir}/usr/bin/airdrop-ng
	chmod +x ${pkgdir}/usr/bin/airdrop-ng
	
	# airgraph-ng libs
	install -Dm644 airgraph-ng/lib/lib_Airgraphviz.py \
		${pkgdir}/usr/lib/python2.7/site-packages/	
	
	# airgraph-ng
	sed s/python/python2/ -i airgraph-ng/airgraph-ng.py
	install -Dm644 airgraph-ng/airgraph-ng.py ${pkgdir}/usr/bin/airgraph-ng
	chmod +x ${pkgdir}/usr/bin/airgraph-ng

	# airmon-ng	
	install -Dm644 airmon-ng ${pkgdir}/usr/bin/
	
	# airodump-ng-oui-update
	install -Dm644 airodump-ng-oui-update ${pkgdir}/usr/bin/
}
