# SPDX-License-Identifier: AGPL-3.0

#    ----------------------------------------------------------------------
#    Copyright © 2024, 2025  Pellegrino Prevete
#
#    All rights reserved
#    ----------------------------------------------------------------------
#
#    This program is free software: you can redistribute it and/or modify
#    it under the terms of the GNU Affero General Public License as published by
#    the Free Software Foundation, either version 3 of the License, or
#    (at your option) any later version.
#
#    This program is distributed in the hope that it will be useful,
#    but WITHOUT ANY WARRANTY; without even the implied warranty of
#    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
#    GNU Affero General Public License for more details.
#
#    You should have received a copy of the GNU Affero General Public License
#    along with this program.  If not, see <https://www.gnu.org/licenses/>.

# Maintainers:
#   Truocolo
#     <truocolo@aol.com>
#     <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
#   Pellegrino Prevete (dvorak)
#     <pellegrinoprevete@gmail.com>
#     <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
# Contributors:
#   Filipe Bertelli
#     <filipebertelli@tutanota.com>

_os="$(
  uname \
    -o)"
_arch="$(
  uname \
    -m)"
_evmfs_available="$(
  command \
    -v \
    "evmfs" || \
    true)"
if [[ ! -v "_evmfs" ]]; then
  if [[ "${_evmfs_available}" != "" ]]; then
    _evmfs="true"
  elif [[ "${_evmfs_available}" == "" ]]; then
    _evmfs="false"
  fi
fi
if [[ ! -v "_npm" ]]; then
  if [[ "${_evmfs}" == "true" ]]; then
    _npm="false"
  elif [[ "${_evmfs}" == "false" ]]; then
    _npm="false"
  fi
fi
if [[ ! -v "_git" ]]; then
  if [[ "${_evmfs}" == "false" ]]; then
    _git="false"
  elif [[ "${_evmfs}" == "true" ]]; then
    _git="false"
  fi
fi
if [[ ! -v "_git_service" ]]; then
  if [[ "${_evmfs}" == "false" ]]; then
    _git_service="github"
  elif [[ "${_evmfs}" == "true" ]]; then
    _git_service="github"
  fi
fi
if [[ ! -v "_offline" ]]; then
  _offline='false'
fi
if [[ ! -v "_pub" ]]; then
  _pub="nomicfoundation"
  if [[ "${_os}" == "Android" ]]; then
    _pub="nomicfoundation"
  fi
  _pub="themartiancompany"
fi
if [[ ! -v "_ns" ]]; then
  _ns="NomicFoundation"
  # Android support
  _ns="themartiancompany"
fi
if [[ ! -v "_platform" ]]; then
  if [[ "${_os}" == "Android" ]]; then
    elif [[ "${_arch}" == "aarch64" ]]; then
      _platform="android-arm-eabi"
    if [[ "${_arch}" == "armv8l" ]]; then
      _platform="android-aarch64"
    if [[ "${_arch}" == "armv7l" ]]; then
      _platform="android-arm-eabi"
    elif [[ "${_arch}" == "i686" ]]; then
      _platform="android-x86_64"
    elif [[ "${_arch}" == "x86_64" ]]; then
      _platform="android-x86_64"
    fi
  elif [[ "${_os}" == "GNU/Linux" ]]; then
    if [[ "${_arch}" == "x86_64" ]]; then
      _platform="gnu-x86_64"
    fi
  elif [[ "${_os}" == "Msys" ]]; then
    if [[ "${_arch}" == "x86_64" ]]; then
      _platform="windows-x86_64"
    fi
  fi
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_npm}" == "true" ]]; then
      _archive_format="tgz"
    elif [[ "${_npm}" == "false" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        _archive_format="zip"
      elif [[ "${_git_service}" == "gitlab" ]]; then
        _archive_format="tar.gz"
      fi
    fi
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
pkgver="${_pkgver}.1.1.1"
_commit="a45f6027efccc03125160aff83e582f37a3f11c0"
pkgrel=21
arch=(
  'aarch64'
  'arm'
  'armv8l'
  'armv7l'
  'i686'
  'mips'
  'powerpc'
  'pentium4'
  'x86_64'
)
url="https://${_git_service}.com/${_ns}/${_pkgbase}"
license=(
  'custom'
)
depends=(
  "${_node}"
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
if [[ "${_npm}" == "true" ]]; then
  _tag="${pkgver}"
  _tag_name="pkgver"
elif [[ "${_npm}" == "false" ]]; then
  _tag="${_commit}"
  _tag_name="commit"
fi
_tarname="${pkgname}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
if [[ "${_offline}" == "true" ]]; then
  _url="file://${HOME}/${pkgname}"
fi
_bundle_sum="SKIP"
_bundle_sig_sum="SKIP"
_gitlab_sum="SKIP"
_gitlab_sig_sum="SKIP"
_github_sum="a9722d5b554215deef6b2a190995e9937647173411d577f277bb00c481fec8d9"
_github_sig_sum="e35f0b9b378453f0edabb0282a39dfd2de2b8161d0262b44462c8fb2e4ccca6a"
if [[ "${_git_service}" == "github" ]]; then
  _evmfs_sum="${_github_sum}"
  _evmfs_sig_sum="${_github_sig_sum}"
elif [[ "${_git_service}" == "gitlab" ]]; then
  _evmfs_sum="${_gitlab_sum}"
  _evmfs_sig_sum="${_gitlab_sig_sum}"
fi
_npm_sum="SKIP"
_npm_sig_sum="SKIP"
# Truocolo
_evmfs_ns="0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b"
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_evmfs_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_bundle_uri="${_evmfs_dir}/${_bundle_sum}"
_bundle_src="${_tarfile}::${_bundle_uri}"
_evmfs_npm_uri="${_evmfs_dir}/${_npm_sum}"
_evmfs_npm_src="${_tarfile}::${_evmfs_npm_uri}"
_evmfs_sig_uri="${_evmfs_dir}/${_evmfs_sig_sum}"
_evmfs_sig_src="${_tarfile}.sig::${_evmfs_sig_uri}"
_bundle_sig_uri="${_evmfs_dir}/${_bundle_sig_sum}"
_bundle_sig_src="${_tarfile}.sig::${_bundle_sig_uri}"
_npm_sig_uri="${_evmfs_dir}/${_npm_sig_sum}"
_npm_sig_src="${_tarfile}.sig::${_npm_sig_uri}"
_npm_http="http://registry.npmjs.org"
source=()
sha256sums=()
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_npm}" == "true" ]]; then
    _uri="${_evmfs_npm_uri}"
    _sum="${_npm_sum}"
    _sig_src="${_npm_sig_src}"
    _sig_sum="${_npm_sig_sum}"
  elif [[ "${_npm}" == "false" ]]; then
    if [[ "${_git}" == "true" ]]; then
      _uri="${_bundle_uri}"
      _sum="${_bundle_sum}"
      _sig_src="${_bundle_sig_src}"
      _sig_sum="${_bundle_sig_sum}"
    elif [[ "${_git}" == "false" ]]; then
      if [[ "${_git_service}" == "github" ]]; then
        _sum="${_github_sum}"
        _sig_sum="${_github_sig_sum}"
      fi
      _uri="${_evmfs_uri}"
      _sig_src="${_evmfs_sig_src}"
    fi
  fi
  source+=(
    "${_sig_src}"
  )
  sha256sums+=(
    "${_sig_sum}"
  )
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_npm}" == "true" ]]; then
    _uri="${_npm_http}/@${_ns}/${_pkg}/-/${_tarfile}"
    _sum="${_npm_sum}"
  elif [[ "${_npm}" == "false" ]]; then
    if [[ "${_git}" == true ]]; then
      _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
      _sum="SKIP"
    elif [[ "${_git}" == false ]]; then
      _uri=""
      if [[ "${_git_service}" == "github" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}/archive/${_commit}.${_archive_format}"
          _sum="${_github_sum}"
        fi
      elif [[ "${_git_service}" == "gitlab" ]]; then
        if [[ "${_tag_name}" == "commit" ]]; then
          _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
          _sum="${_gitlab_sum}"
        fi
      fi
      _src="${_tarfile}::${_uri}"
    fi
  fi
fi
_src="${_tarfile}::${_uri}"
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
if [[ "${_npm}" == "true" ]]; then
  noextract=(
    "${_tarfile}"
  )
fi
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  'DD6732B02E6C88E9E27E2E0D5FC6652B9D9A6C01'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

_android_quirk() {
  local \
    _tools_bin \
    _clang \
    _compiler_dir \
    _compiler
  cd \
    "${srcdir}/${_tarname}"
  if [[ "${_os}" == "Android" ]]; then
    _tools_bin="undefined/toolchains/llvm/prebuilt/linux-x86_64/bin"
    _compiler_dir="${srcdir}/${_tarname}/${_tools_bin}"
    if [[ "${_arch}" == "aarch64"  ]]; then
      _compiler="${_compiler_dir}/${_arch}-linux-android24-clang"
    elif [[ "${_arch}" == "armv7l" || \
          "${_arch}" == "armv8l" ]]; then
      _compiler="${_compiler_dir}/armv7a-linux-androideabi24-clang"
    fi
    _clang="$( \
      command \
        -v \
        "clang")"
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

_msys_quirk() {
  local \
    _tools_bin \
    _clang \
    _compiler_dir \
    _compiler
  cd \
    "${srcdir}/${_tarname}"
  if [[ "${_os}" == "Msys" ]]; then
    _clang="$( \
      command \
        -v \
        gcc)"
    ls \
      "undefined/toolchains/llvm-prebuilt"
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
  local \
    _yarn
  _yarn=( "$(
    command \
      -v \
      "yarn" || \
    true)"
  )
  cd \
    "${srcdir}/${_tarname}"
  mkdir \
    -p \
    "build"
  cp \
    "yarn.lock" \
    "build"
  npm \
    install \
    . || \
    true
  if [[ "${_yarn[*]}" == "" ]]; then
    npm \
      install \
        "yarn" || \
      true
    _yarn=(
      npx
        "yarn"
    )
  fi
  "${_yarn[@]}" \
    install || \
    true
  npm \
    install \
    --package-lock-only || \
    true
  _android_quirk
  "${_yarn[@]}" \
    run \
      build || \
  ( "${_yarn[@]}" \
      install && \
    "${_yarn[@]}" \
      run \
        build )
  ls \
    -lsh
  if [[ -e "solidity-analyzer.${_platform}.node" ]]; then
    if [[ "${_os}" == "Android" && \
          "${_arch}" == "armv7l" ]]; then
      echo \
        "Android ARM 32 build."
    fi
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
  else
    _tgz="${_pub}-${_pkg}-${_pkgver}.tgz"
    npm \
      "${_npm_options[@]}" \
      install \
        "${_tgz}"
  fi
}

# vim:set sw=2 sts=-1 et:
