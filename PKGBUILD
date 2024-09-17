# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Contributor: Filipe Bertelli <filipebertelli@tutanota.com>

_source='npm'
_ns="NomicFoundation"
_pub="@nomicfoundation"
_os="$( \
  uname \
    -o)"
if [[ "${_os}" == "Android" ]]; then
  _source="ur"
fi
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
_commit="925641061bd7fc0cfac07395353c14147f29e1d0"
pkgrel=1
arch=(
  'any'
)
if [[ "${_source}"= = "ur" ]]; then
  _ns="themartiancompany"
fi
url="https://github.com/${_ns}/${_pkgbase}"
license=(
  'custom'
)
depends=(
  'nodejs'
)
makedepends=(
  'npm'
)
source=(
)
sha512sums=(
)
if [[ "${_source}"= = "ur" ]]; then
  _tar="${_tarname}.zip::${_url}/archive/${_commit}.zip"
  source+=(
    "${_tar}"
  )
  sha512sums+=(
    'ab89f7dbf14d288850df34061b0e42bcf17a193bc30a963021fedb118fdd65365b81f0ec1f28c9c144715097f7550bae263f9f0c8165e3e2a40556f0e047fa8c'
  )
elif [[ "${_source}"= = "npm" ]]; then
  _npm="http://registry.npmjs.org"
  source+=(
    "${_npm}/${_pub}/${_pkgbase}/-/${_pkgbase}-${pkgver}.tgz"
  )
  sha512sums+=(
    'ab89f7dbf14d288850df34061b0e42bcf17a193bc30a963021fedb118fdd65365b81f0ec1f28c9c144715097f7550bae263f9f0c8165e3e2a40556f0e047fa8c'
  )
  noextract=(
    "${_pkgbase}-${pkgver}.tgz"
  )
fi


package() {
  local \
    _npm_options=() \
    _tgz
  _npm_options=(
    -g
    # --user=root
    --prefix="${pkgdir}/usr"
  )
  if [[ "${_source}" == "npm" ]]; then
    _tgz="${srcdir}/${_pkgbase}-${pkgver}.tgz"
  elif [[ "${_source}" == "ur" ]]; then
    cd \
      ${pkgbase}
    npm \
      pack
    _tgz="$( \
      ls \
        *.tgz)"
  fi
  npm \
    install \
      "${_npm_options[@]}" \
      "${_tgz}"
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
