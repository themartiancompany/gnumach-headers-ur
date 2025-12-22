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
#   Luca Weiss
#     <luca@z3ntu.xyz>

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
if [[ ! -v "_git" ]]; then
  _git="true"
fi
if [[ ! -v "_offline" ]]; then
  _offline="false"
fi
if [[ ! -v "_archive_format" ]]; then
  if [[ "${_git}" == "true" ]]; then
    if [[ "${_evmfs}" == "true" ]]; then
      _archive_format="bundle"
    elif [[ "${_evmfs}" == "false" ]]; then
      _archive_format="git"
    fi
  elif [[ "${_git}" == "false" ]]; then
    if [[ "${_git_http}" == "github" ]]; then
      _archive_format="zip"
    elif [[ "${_git_http}" == "gitlab" ]]; then
      _archive_format="tar.gz"
    fi
  fi
fi
_libc="glibc"
if [[ ! -v "_c_compiler" ]]; then
  _c_compiler="gcc"
  _c_compiler_lib="lib32-gcc-libs"
  if [[ "${_os}" == "Android" ]]; then
    _c_compiler="clang"
    _c_compiler_lib="llvm-libs"
  fi
fi
_proj=gnu
_name=mach
_pkg=${_proj}${_name}
_component=headers
pkgbase="${_pkg}-${_component}"
pkgname=(
  "${pkgbase}"
)
pkgver=1.8.r82.g0294ec07
# branch 'master' in hurd/gnumach.git
_commit="0294ec07a1655b2883afae5877eb9111a7f3a343"
_bundle_commit="8908b9977efc334bf74ffa79923dc8b05fef9748"
pkgrel=11
pkgdesc="GNU Mach - header files"
arch=(
  'arm'
  'aarch64'
  'i686'
  'x86_64'
)
_ns="hurd"
url="https://www.${_proj}.org/software/${_ns}/microkernel/${_name}.html"
license=(
  'GPL'
)
groups=(
  'base-devel'
  "${_proj}"
)
depends=(
  "${_libc}"
)
makedepends=(
  "autoconf"
  "automake"
  "${_c_compiler}"
  "make"
  "patch"
)
if [[ "${_arch}" == "x86_64" ]]; then
  makedepends+=(
    "${_c_compiler_lib}"
  )
fi
if [[ " ${_options[*]} " == *" debug "* ]]; then
  makedepends+=(
    "debugedit"
  )
fi
if [[ "${_git}" == "true" ]]; then
  makedepends+=(
    "git"
  )
fi
_http="https://git.savannah.${_proj}.org/git"
_url="${_http}/${_ns}/${_pkg}.git"
_tag_name="commit"
_tag="${_commit}"
_tarname="${_pkg}-${_tag}"
_tarfile="${_tarname}.${_archive_format}"
_bundle_sum="1daa1027c12aedb723e467dcd08902bab7a780419cea24df62e3409a22797460"
_bundle_sig_sum="771c1d1e74a5c077a8a3dc804e30be9c0c012d7098d9d46e0100a5a448cc1e84"
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="${_bundle_sum}"
    _sig_sum="${_bundle_sig_sum}"
  elif [[ "${_git}" == "false" ]]; then
    _sum="SKIP"
    _sig_sum="SKIP"
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _sum="SKIP"
    _sig_sum="SKIP"
  fi
fi
# Dvorak
_evmfs_ns="0x87003Bd6C074C713783df04f36517451fF34CBEf"
# Tallero
_evmfs_ns="0x6ec7cC56dCeC0a00CB15E97C64B1a5Ec7A31403c"
_evmfs_network="100"
_evmfs_address="0x69470b18f8b8b5f92b48f6199dcb147b4be96571"
_evmfs_dir="evmfs://${_evmfs_network}/${_evmfs_address}/${_evmfs_ns}"
_evmfs_uri="${_evmfs_dir}/${_sum}"
_evmfs_src="${_tarfile}::${_evmfs_uri}"
_sig_uri="${_evmfs_dir}/${_sig_sum}"
_sig_src="${_tarfile}.sig::${_sig_uri}"
source=()
sha256sums=()
if [[ "${_evmfs}" == "true" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _src="${_evmfs_src}"
    source+=(
      "${_sig_src}"
    )
    sha256sums+=(
      "${_sig_sum}"
    )
  fi
elif [[ "${_evmfs}" == "false" ]]; then
  if [[ "${_git}" == "true" ]]; then
    _src="${_tarname}::git+${_url}#${_tag_name}=${_tag}?signed"
    _sum="SKIP"
  elif [[ "${_git}" == false ]]; then
    _uri=""
    if [[ "${_git_http}" == "github" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/archive/${_commit}.${_archive_format}"
        _sum="${_github_sum}"
      fi
    elif [[ "${_git_http}" == "gitlab" ]]; then
      if [[ "${_tag_name}" == "commit" ]]; then
        _uri="${_url}/-/archive/${_tag}/${_tag}.${_archive_format}"
      fi
    fi
    _src="${_tarfile}::${_uri}"
  fi
fi
source+=(
  "${_src}"
)
sha256sums+=(
  "${_sum}"
)
validpgpkeys=(
  # Truocolo
  #   <truocolo@aol.com>
  '97E989E6CF1D2C7F7A41FF9F95684DBE23D6A3E9'
  #   <truocolo@0x6E5163fC4BFc1511Dbe06bB605cc14a3e462332b>
  'F690CBC17BD1F53557290AF51FC17D540D0ADEED'
  # Pellegrino Prevete (dvorak)
  #   <dvorak@0x87003Bd6C074C713783df04f36517451fF34CBEf>
  '12D8E3D7888F741E89F86EE0FEC8567A644F1D16'
)

pkgver() {
  cd \
    "${_tarname}"
  git \
    describe \
    --long | \
    sed \
      's/^v//;s/\([^-]*-g\)/r\1/;s/-/./g'
}

prepare() {
  rm \
    -rf \
    "build"
  mkdir \
    "build"
  cd \
    "${_tarname}"
  autoreconf \
    -fi
}

build() {
  local \
    _configure_opts=() \
    _build_platform \
    _host_platform
  if [[ "${_os}" == "GNU/Linux" ]]; then
    if [[ "${_arch}" == "x86_64" ]]; then
      _build_platform="${_arch}-pc-linux-gnu"
      _host_platform="i386-gnu"
    fi
  fi
  _configure_opts+=(
    --build="${_build_platform}"
    --host="${_host_platform}"
    --prefix="/usr"
    --libexecdir="/usr/lib"
  )
  cd \
    "build"
  "../${_tarname}/configure" \
    "${_configure_opts[@]}" || \
    true
  echo "The Makefile"
  cat \
    "${srcdir}/Makefile.in"
  # find \
  #   "${srcdir}" \
  #   -type \
  #     "f" \
  #   -iname \
  #     "config.status.dep.patch" | \
  #   -exec \
  #     cat \
  #       '{}' \; || \
  #   true
}

package() {
  local \
    _make_opts=()
  _make_opts+=(
    DESTDIR="${pkgdir}"
  )
  cd \
    "build"
  make \
    "${_make_opts[@]}" \
    install-data
}
