# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Contributor: Filipe Bertelli <filipebertelli@tutanota.com>

_pub="@nomicfoundation"
_pkgbase=solidity-analyzer
pkgname="${_pkgbase}"
_pkgdesc=(
  'API library built in Rust,'
  'which exposes a single function,'
  'which takes the contents of a Solidity source file'
  'and returns its imports and version pragmas'
)
pkgdesc="${_pkgdesc[*]}"
pkgver=0.1.2
pkgrel=1
arch=(
  'any'
)
_ns="NomicFoundation"
url="https://github.com/${_ns}/${_pkgbase}"
license=(
  'custom'
)
depends=(
  'nodejs'
  'inherits'
)
makedepends=(
  'npm'
)
_npm="http://registry.npmjs.org"
source=(
  "${_npm}/${_pub}/${_pkgbase}/-/${_pkgbase}-${pkgver}.tgz"
)
noextract=(
  "${_pkgbase}-${pkgver}.tgz"
)
sha512sums=(
  'ab89f7dbf14d288850df34061b0e42bcf17a193bc30a963021fedb118fdd65365b81f0ec1f28c9c144715097f7550bae263f9f0c8165e3e2a40556f0e047fa8c'
)

package() {
  local \
    _npm_options=()
  _npm_options=(
    -g
    # --user=root
    --prefix="${pkgdir}/usr"
    )
  npm \
    install \
      "${_npm_options[@]}" \
      "${srcdir}/${_pkgbase}-${pkgver}.tgz"
  rm \
    -fr \
      "${pkgdir}/usr/etc"
  # Fix npm derp
  find \
    "${pkgdir}/usr" \
    -type d \
    -exec \
      chmod \
        755 \
	'{}' \
	+
}

# vim:set sw=2 sts=-1 et:
