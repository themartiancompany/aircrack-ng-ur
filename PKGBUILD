# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Maintainer: Jonathan Steel <jsteel at archlinux.org>
# Contributor: Brad Fanella <bradfanella@archlinux.us>
# Contributor: Daenyth <Daenyth+Arch [at] gmail [dot] com>
# Contributor: Corrado Primier <bardo@aur.archlinux.org>
# Contributor: ice-man <icemanf@gmail.com>

_os="$( \
  uname \
  -o)"
_hwloc='true'
_usbutils='true'
_py="python"
[[ "${_os}" == 'Android' ]] && \
  _hwloc='false' \
  _usbutils='false'
pkgname=aircrack-ng
_pkgver=1.7
pkgver=${_pkgver//-/}
pkgrel=4
pkgdesc="Key cracker for the 802.11 WEP and WPA-PSK protocols"
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'i686'
)
url="https://www.${pkgname}.org"
license=(
  'GPL2'
)
depends=(
  'glibc'
  'gcc-libs'
  'openssl'
  'sqlite'
  'iw'
  'net-tools'
  'wireless_tools'
  'ethtool'
  'pcre'
  'libpcap'
  libpcap.so
  "${_py}"
  'zlib'
  'libnl'
)
[[ "${_usbutils}" == 'true' ]] && \
  depends+=(
    'usbutils'
  )
[[ "${_hwloc}" == 'true' ]] && \
  depends+=(
    'hwloc'
  )
makedepends=(
  "${_py}-setuptools"
)
checkdepends=(
  'cmocka'
)
conflicts=(
  "${pkgname}-scripts"
)

replaces=(
  "${pkgname}-scripts"
)
provides=(
  "${pkgname}-scripts"
)
source=(
  "https://download.${pkgname}.org/${pkgname}-${_pkgver}.tar.gz"
)
sha256sums=(
  '05a704e3c8f7792a17315080a21214a4448fd2452c1b0dd5226a3a55f90b58c3'
)
b2sums=(
  '4461af7b698d30c96e6f93494d5ee658bf8d7144d8b165e9b8aee1766a35dddded3bbb738237e1100dcf22167125aa7cf9149288bba1607fe778470b04596cb2'
)

prepare() {
  cd \
    "${pkgname}-${_pkgver}"
  autoreconf \
    -fiv
}

_get_usr() {
  local \
    _usr \
    _bin
  _bin="$( \
    dirname \
      "$( \
        command \
          -v \
          "cc")")"
  _usr="$( \
    dirname \
      "${_bin}")"
  echo \
    "$( \
      realpath \
        "${_usr}")"
}

build() {
  local \
    _configure_opts=() \
    _usr
  _usr="$( \
    _get_usr)"
  _configure_opts=(
    --prefix="${_usr}"
    --libexecdir="${_usr}/lib"
    --sbindir="${_usr}/bin"
    --with-ext-scripts
    --with-experimental
  )
  if [[ "${_hwloc}" != 'true' ]]; then
    _configure_opts+=(
      --disable-hwloc
    )
  fi
  cd \
    "${pkgname}-${_pkgver}"
  ./configure \
    "${_configure_opts[@]}"
  make
}

check() {
  cd \
    "${pkgname}-${_pkgver}"
  make \
    check
}

package() {
  cd \
    "${pkgname}-${_pkgver}"
  make \
    DESTDIR="${pkgdir}" \
    PREFIX='/usr' \
    install
  if \
    [[ "${_os}" == "Android" ]]; then
    mv \
      "${pkgdir}/data/data/com.termux/files/"* \
      "${pkgdir}"
    rm \
      -r \
      "${pkgdir}/data"
  fi
}

# vim: ts=2 sw=2 et:
