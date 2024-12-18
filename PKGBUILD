# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Pellegrino Prevete <pellegrinoprevete@gmail.com>
# Maintainer: Truocolo <truocolo@aol.com>
# Contributor: Filipe Bertelli <filipebertelli@tutanota.com>

_offline='false'
_source='ur'
_ns="NomicFoundation"
_pub="nomicfoundation"
_os="$( \
  uname \
    -o)"
_arch="$( \
  uname \
    -m)"
if [[ "${_os}" == "Android" ]]; then
  _source="ur"
  if [[ "${_arch}" == "armv7l" ]]; then
    _platform="android-arm-eabi"
  fi
fi
_node="nodejs"
_pkg=solidity-analyzer
_pkgbase="${_pkg}"
pkgname="${_pkgbase}"
_pkgdesc=(
  'API library built in Rust,'
  'which exposes a single function,'
  'which takes the contents of a Solidity source file'
  'and returns its imports and version pragmas'
)
pkgdesc="${_pkgdesc[*]}"
_pkgver="0.1.2"
pkgver="${_pkgver}.1.1"
_commit="55a88c2957de8f93af3bb135187fc2c7a0973291"
pkgrel=1
arch=(
  'x86_64'
  'arm'
  'aarch64'
  'i686'
  'mips'
  'powerpc'
  'pentium4'
)
if [[ "${_source}" == "ur" ]]; then
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
  'rust'
  'yarn'
)
provides=(
  "${_node}-${_pkg}=${pkgver}"
)
conflicts=(
  "${_node}-${_pkg}=${pkgver}"
)
source=(
)
sha256sums=(
)
_url="${url}"
_tag="${_commit}"
_tag_name="commit"
_tarname="${pkgname}-${_tag}"
[[ "${_offline}" == "true" ]] && \
  _url="file://${HOME}/${pkgname}"
if [[ "${_source}" == "ur" ]]; then
  _tar="${_tarname}.zip::${_url}/archive/${_commit}.zip"
  source+=(
    "${_tar}"
  )
  _sum="31a540388e9fd4e54e6a5c7ef0ff8ed042a404994519212e2524a93a2a282254"
  sha256sums+=(
    "${_sum}"
  )
elif [[ "${_source}" == "npm" ]]; then
  _npm="http://registry.npmjs.org"
  source+=(
    "${_npm}/@${_pub}/${_pkgbase}/-/${_pkgbase}-${pkgver}.tgz"
  )
  sha256sums+=(
    'ab89f7dbf14d288850df34061b0e42bcf17a193bc30a963021fedb118fdd65365b81f0ec1f28c9c144715097f7550bae263f9f0c8165e3e2a40556f0e047fa8c'
  )
  noextract=(
    "${_pkgbase}-${pkgver}.tgz"
  )
fi

_android_quirk() {
  local \
    _tools_bin \
    _clang \
    _compiler_dir \
    _compiler
  cd \
    "${srcdir}/${_tarname}"
  if [[ "${_os}" == "Android" ]] && \
     [[ "${_arch}" == "armv7l" ]]; then
    _clang="$( \
      command \
        -v \
        clang)"
    _tools_bin="undefined/toolchains/llvm/prebuilt/linux-x86_64/bin"
    _compiler_dir="${srcdir}/${_tarname}/${_tools_bin}"
    _compiler="${_compiler_dir}/armv7a-linux-androideabi24-clang"
    mkdir \
      -p \
      "${_compiler_dir}"
    ln \
      -s \
      "${_clang}" \
      "${_compiler}" || \
      true
  fi
  cd \
    "${srcdir}/${_tarname}"
}

prepare() {
  _android_quirk
}

build() {
  cd \
    "${srcdir}/${_tarname}"
  npm \
    install \
    . || \
    true
  yarn || \
    true
  npm \
    install \
    . || \
    true
  yarn \
    install || \
    true
  _android_quirk
  echo \
    "$(pwd)"
  yarn \
    run \
      build
  if [[ "${_os}" == "Android" ]] && \
     [[ "${_arch}" == "armv7l" ]]; then
    mv \
      "solidity-analyzer.${_platform}.node" \
      "npm/${_platform}" || \
      true
    cd \
      "npm/${_platform}"
    npm \
      pack
    cd \
      "${srcdir}/${_tarname}"
  fi
  npm \
    pack
}

package() {
  local \
    _npm_options=() \
    _tgz
  _npm_options=(
    -g
    # --user=root
    --prefix="${pkgdir}/usr"
  )
  cd \
    "${srcdir}/${_tarname}"
  if [[ "${_os}" == "Android" ]] && \
     [[ "${_arch}" == "armv7l" ]]; then
    cd \
      "npm/${_platform}"
    _tgz="${_pub}-${_pkg}-${_platform}-${_pkgver}.tgz"
    npm \
      "${_npm_options[@]}" \
      install \
        "${_tgz}"
    cd \
      "${srcdir}/${_tarname}"
  fi
  _tgz="${_pub}-${_pkg}-${_pkgver}.tgz"
  npm \
    "${_npm_options[@]}" \
    install \
      "${_tgz}"
}

# vim:set sw=2 sts=-1 et:
