# Maintainer: Brad Fanella <bradfanella@archlinux.us>
# Contributor:  Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

pkgbase=aircrack-ng
pkgname=(aircrack-ng aircrack-ng-scripts)
pkgver=1.1
pkgrel=8
arch=('i686' 'x86_64')
url="http://www.aircrack-ng.org"
license=('GPL2')
source=("http://download.aircrack-ng.org/${pkgname}-${pkgver}.tar.gz")
md5sums=('f7a24ed8fad122c4187d06bfd6f998b4')
depends=('openssl' 'sqlite3' 'iw' 'net-tools')

build() {
  	cd ${srcdir}/${pkgbase}-${pkgver}
  	make SQLITE=true unstable=true
}

package_aircrack-ng() {
	pkgdesc="A key cracker for the 802.11 WEP and WPA-PSK protocols"

  	cd ${srcdir}/${pkgname}-${pkgver}
	make DESTDIR=${pkgdir} SQLITE=true unstable=true bindir=/usr/bin  \
		mandir=/usr/share/man/man1 sbindir=/usr/sbin install

	### Remove installed scripts/corresponding man pages (installed in aircrack-ng-scripts) ###
	# Scripts
	rm ${pkgdir}/usr/sbin/airdriver-ng
	rm ${pkgdir}/usr/sbin/airodump-ng-oui-update
	# Man pages
	mkdir -p ${srcdir}/tmp/
	mv ${pkgdir}/usr/share/man/man1/airdriver-ng.1 ${srcdir}/tmp/
}

package_aircrack-ng-scripts() {
	pkgdesc="Included scripts for a key cracker for the 802.11 WEP and WPA-PSK protocols"
        depends=('python2' 'graphviz' 'python2-pylorcon')	

	cd ${srcdir}/aircrack-ng-${pkgver}/scripts
	mkdir -p ${pkgdir}/usr/share/man/man1/ \
		${pkgdir}/usr/sbin

	### AIRDRIVER-NG ###
	# Script
	install -Dm644 airdriver-ng ${pkgdir}/usr/sbin/
	# Libs
	mkdir -p ${pkgdir}/usr/lib/airdrop-ng/
	install -Dm644 airdrop-ng/lib/{colorize.py,libDumpParse.py,libOuiParse.py} \
		${pkgdir}/usr/lib/airdrop-ng/
	# Man page
	mv ${srcdir}/tmp/airdriver-ng.1 ${pkgdir}/usr/share/man/man1/

	### AIRDROP-NG ### 
	# Man page
	install -Dm644 airdrop-ng/docs/airdrop-ng.1 ${pkgdir}/usr/share/man/man1/ 
	# Script
	sed s/python/python2/ -i airdrop-ng/airdrop-ng.py
	install -Dm644 airdrop-ng/airdrop-ng.py ${pkgdir}/usr/sbin/airdrop-ng
	chmod +x ${pkgdir}/usr/sbin/airdrop-ng
	
	### AIRGRAPH-NG ###
	# Libs
	mkdir -p ${pkgdir}/usr/lib/airgraph-ng/
	install -Dm644 airgraph-ng/lib/lib_Airgraphviz.py \
		${pkgdir}/usr/lib/airgraph-ng/
	# Man page
	install -Dm644 airgraph-ng/man/airgraph-ng.1 ${pkgdir}/usr/share/man/man1/	
	# Script
	sed s/python/python2/ -i airgraph-ng/airgraph-ng.py
	sed s_/usr/local/bin/lib_/usr/lib_ -i airgraph-ng/airgraph-ng.py
	install -Dm644 airgraph-ng/airgraph-ng.py ${pkgdir}/usr/sbin/airgraph-ng
	chmod +x ${pkgdir}/usr/sbin/airgraph-ng

	### DUMP-JOIN.PY ###
	# Man page
	install -Dm644 airgraph-ng/man/dump-join.1 ${pkgdir}/usr/share/man/man1/
	# Script
	sed s/python/python2/ -i airgraph-ng/dump-join.py
	install -Dm644 airgraph-ng/dump-join.py ${pkgdir}/usr/sbin/dump-join.py
	chmod +x ${pkgdir}/usr/sbin/dump-join.py
	
	### AIRODUMP-NG-OUI-UPDATE ###
	# Script
	install -Dm644 airodump-ng-oui-update ${pkgdir}/usr/sbin/
	chmod +x ${pkgdir}/usr/sbin/airodump-ng-oui-update

}
