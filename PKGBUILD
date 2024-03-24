# Maintainer: Some One <some.one@some.email.com>

_realname=libdatachannel-python
pkgbase=mingw-w64-libdatachannel
pkgname=("${MINGW_PACKAGE_PREFIX}-${_realname}")
pkgver=0.20.2
pkgrel=1
pkgdesc="Python bindings to libdatahannel"
arch=('x86_64')
mingw_arch=('mingw64' 'ucrt64' 'clang64' 'clangarm64')
depends=("${MINGW_PACKAGE_PREFIX}-gcc-libs" "${MINGW_PACKAGE_PREFIX}-openssl" )
url="https://github.com/wusspuss/$_realname"
license=('MPL2')
makedepends=("${MINGW_PACKAGE_PREFIX}-python-cffi"
             'git')

source=("git+https://github.com/wusspuss/libdatachannel-python.git")
sha256sums=('SKIP')

prepare() {
  cd "${srcdir}"
  rm -rf python-build-${MSYSTEM} | true
  cp -r "${_realname}" "python-build-${MSYSTEM}"
}



build() {
    cd "${srcdir}/python-build-${MSYSTEM}"
    python -m build --wheel --no-isolation
}

package() {
    cd "${srcdir}/python-build-${MSYSTEM}"

    MSYS2_ARG_CONV_EXCL="--prefix=" \
		       ${MINGW_PREFIX}/bin/python -m installer --prefix=${MINGW_PREFIX} \
		       --destdir="${pkgdir}" dist/*.whl
}
