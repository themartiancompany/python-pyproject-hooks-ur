# SPDX-License-Identifier: AGPL-3.0
#
# Maintainer: Truocolo <truocolo@aol.com>
# Maintainer: Pellegrino Prevete (tallero) <pellegrinoprevete@gmail.com>
# Maintainer: David Runge <dvzrv@archlinux.org>

_py="python"
_pyver="$( \
  "${_py}" \
    -V | \
    awk \
      '{print $2}')"
_pymajver="${_pyver%.*}"
_pyminver="${_pymajver#*.}"
_pynextver="${_pymajver%.*}.$(( \
  ${_pyminver} + 1))"
_pkg=pyproject-hooks
pkgname="${_py}-${_pkg}"
pkgver=1.1.0
pkgrel=1
pkgdesc="A low-level library for calling build-backends in pyproject.toml-based project"
arch=(
  any
)
_http="https://github.com"
_ns="pypa"
url="${_http}/${_ns}/${_pkg}"
license=(
  MIT
)
depends=(
  "${_py}>=${_pymajver}"
  "${_py}<${_pynextver}"
)
makedepends=(
  "${_py}-build"
  "${_py}-installer"
  "${_py}-flit-core"
  "${_py}-wheel"
)
checkdepends=(
  "${_py}-pytest"
  "${_py}-setuptools"
  "${_py}-testpath"
)
source=(
  "${pkgname}-${pkgver}.tar.gz::${url}/archive/refs/tags/v${pkgver}.tar.gz"
)
sha512sums=(
  '256028d13adbe35126a63431a2a49e0c48adddce5ffc3ff2eebad368eee7ce52591ecfd8a8526876de20bc59dfc87156533d6a97b55538a739873e60f9509eff'
)
b2sums=(
  'e6b376188655a5bc188567f412c22f8224209612c4fb0332f8c0c441180c18589139549139957834b3359bf3ced961e22f97e2449edc354047afaa6d2eff58d7'
)

build() {
  cd \
    "${_pkg}-${pkgver}"
  "${_py}" \
    -m build \
    --wheel \
    --no-isolation
}

check() {
  cd \
    "${_name}-${pkgver}"
  export \
    PYTHONPATH="$PWD/src:$PYTHONPATH"
  pytest \
    -vv
}

package() {
  cd \
    "${_name}-${pkgver}"
  "${_py}" \
    -m installer \
    --destdir="${pkgdir}" \
    dist/*.whl
  install \
    -vDm 644 \
    LICENSE \
    -t \
    "${pkgdir}/usr/share/licenses/${pkgname}/"
}

# vim: ft=sh syn=sh et
