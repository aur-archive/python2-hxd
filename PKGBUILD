pkgname=python2-hxd
pkgver=29
pkgrel=2
pkgdesc="A hotline server written in python."
url="https://bitbucket.org/jvoss"
arch=(any)
license=("unknown")
depends=(python2)
makedepends=(python2 mercurial)
conflicts=(python-hxd)
provides=(python-hxd)
source=("phxd.sh")
md5sums=('01bf7e23f40303bcabac8857b8731e0e')
_hgroot=$url
_hgrepo=phxd

build() {
cd $srcdir
  msg "Connecting to hg server..."
  if [[ -d "$_hgrepo/.hg" ]]; then
    msg "pull"
    ( cd $_hgrepo && hg pull -u )
  else
    msg "clone"
    hg clone "${_hgroot}/${_hgrepo}"
  fi
  cd "${_hgrepo}"

  msg "Mercurial checkout done or server timeout"
  msg "Starting build..."
  
  rm -rf "${srcdir}/${_hgrepo}-build"
  cp -r "${srcdir}/${_hgrepo}" "${srcdir}/${_hgrepo}-build"
  cd "${srcdir}/${_hgrepo}-build"
  
  sed -i "s:#!/usr/bin/env python:#!/usr/bin/python2:" phxd.py
}

package() {
  cd "$srcdir/${_hgrepo}-build"
  install -Dm755 "phxd.py" "$pkgdir/opt/phxd/phxd.py"
  install -Dm755 "$srcdir/phxd.sh" "$pkgdir/etc/rc.d/phxd"
  cp -r "ssl" "$pkgdir/opt/phxd/"
  mkdir -p "$pkgdir/usr/bin"
  ln -s "/opt/phxd/phxd.py" "$pkgdir/usr/bin/phxd"
}
