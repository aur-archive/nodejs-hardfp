# $Id$
# Maintainer:  Bartłomiej Piotrowski <nospam@bpiotrowski.pl>
# Contributor: Thomas Dziedzic < gostrc at gmail >
# Contributor: James Campos <james.r.campos@gmail.com>
# Contributor: BlackEagle < ike DOT devolder AT gmail DOT com >
# Contributor: Dongsheng Cai <dongsheng at moodle dot com>
# Contributor: Masutu Subric <masutu.arch at googlemail dot com>
# Contributor: TIanyi Cui <tianyicui@gmail.com>
# Contributor: Pedro Lamas <pedrolamas@gmail.com>

pkgname=nodejs-hardfp
pkgver=0.8.8
pkgrel=1
pkgdesc='Evented I/O for V8 javascript'
arch=('arm')
url='http://nodejs.org/'
license=('MIT')
depends=('python2')
checkdepends=('curl') # curl used for check()
optdepends=('openssl: TLS support')
options=('!emptydirs')
source=("http://nodejs.org/dist/v${pkgver}/node-v${pkgver}.tar.gz")
md5sums=('f4dae84e96a94b768404c14633bccd49')

build() {
  cd node-v${pkgver}

  msg 'Fixing for python2 name'
  find -type f -exec sed -e 's_^#!/usr/bin/env python$_&2_' -e 's_^\(#!/usr/bin/python2\).[45]$_\1_' -e 's_^#!/usr/bin/python$_&2_' -e "s_'python'_'python2'_" -i {} \;
  find test -type f -exec sed -e "s|python |python2 |" -i {} \;
  sed -i "s|python |python2 |" Makefile

  export PYTHON=python2

  ./configure \
    --prefix=/usr \
    --shared-openssl

  make
}

check() {
  cd node-v${pkgver}
  make test || true
}

package() {
  cd node-v${pkgver}

  make DESTDIR=${pkgdir} install

  # install docs as per user request
  install -d ${pkgdir}/usr/share/doc/nodejs
  cp -r doc/api/*.html \
    ${pkgdir}/usr/share/doc/nodejs

  install -D -m644 LICENSE \
    ${pkgdir}/usr/share/licenses/nodejs/LICENSE
}

# vim:set ts=2 sw=2 et:
