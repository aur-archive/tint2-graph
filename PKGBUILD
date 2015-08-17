pkgname=tint2-graph
pkgver=652
pkgrel=1
pkgdesc="A basic, good-looking task manager for WMs."
arch=('i686' 'x86_64')
url="http://code.google.com/p/tint2/"
license=('GPL')
depends=('libxcomposite' 'libxdamage' 'libxinerama' 'libxrandr' 'pango' 'imlib2')
makedepends=('cmake' 'subversion')
options=('!libtool')
provides=('tint2')
conflicts=('tint2' 'tint' 'ttm-svn')
source=('graph.patch' 'tint2rc')
md5sums=('82a187a39ca37a5958f62d018bebe42e' '014f9dfdaa93f819cfda97f145c9b5c0')

_svnmod="tint2"
_svntrunk="http://tint2.googlecode.com/svn/trunk"

build() {
  cd ${srcdir}

  msg "Getting sources..."
  if [ -d ${_svnmod}/.svn ]; then
    cd ${_svnmod} && svn up -r ${pkgver}
  else
    svn co ${_svntrunk} --config-dir ./ -r ${pkgver} ${_svnmod}
    cd ${_svnmod}
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting make..."

  patch -p1 < "$srcdir/graph.patch"
  cp "$srcdir/tint2rc" "$srcdir/tint2/sample/tint2rc"

  cmake . -DCMAKE_INSTALL_PREFIX=/usr \
	  -DENABLE_TINT2CONF=0 || return 1

  make || return 1
}

package() {
  cd ${srcdir}/${_svnmod}

  make DESTDIR=${pkgdir} install || return 1
}
