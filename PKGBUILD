# Contributor: demonicmaniac <namida1@gmx.net>
pkgname=sprig-svn
pkgver=15
pkgrel=2
pkgdesc="SDL Primitive Generator" 
arch=(i686 x86_64)
url="http://code.google.com/p/sprig"
license=('LGPL')
depends=('sdl' 'gcc-libs')
makedepends=('svn')
provides=('sprig')
conflicts=('sprig')

_svntrunk="http://sprig.googlecode.com/svn/trunk"
_svnmod="sprig-read-only"

build() {
  
  cd "$srcdir"
  msg "Connecting to SVN server...."

  if [[ -d "$_svnmod/.svn" ]]; then
    (cd "$_svnmod" && svn up -r "$pkgver")
  else
    svn co "$_svntrunk" --config-dir ./ -r "$pkgver" "$_svnmod"
  fi

  msg "SVN checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_svnmod-build"
  cp -r "$srcdir/$_svnmod" "$srcdir/$_svnmod-build"
  cd "$srcdir/$_svnmod-build"

  #
  # BUILD HERE
  #
  mkdir build
  cd build
#  ccmake ../
  cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release ../
  make 
  
}

package() {
	cd "$srcdir/$_svnmod-build/build"
	make DESTDIR="$pkgdir/" install
}

