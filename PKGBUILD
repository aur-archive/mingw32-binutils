# $Id: PKGBUILD 83715 2013-02-04 16:30:55Z spupykin $
# Maintainer: Sergej Pupykin <pupykin.s+arch@gmail.com>
# Maintainer: Ondrej Jirman <megous@megous.com>
# Contributor: mosra <mosra@centrum.cz>

pkgname=mingw32-binutils
pkgver=2.23.1
pkgrel=3
_uprel=1
arch=(i686 x86_64)
url="https://sourceforge.net/projects/mingw/files/MinGW/Base/binutils/"
pkgdesc="A set of programs to assemble and manipulate binary and object files (mingw)"
depends=('glibc' 'zlib')
license=(GPL)
source=("https://downloads.sourceforge.net/project/mingw/MinGW/Base/binutils/binutils-$pkgver/binutils-$pkgver-${_uprel}-mingw32-src.tar.lzma"
	"260cd952.patch::http://sourceware.org/git/?p=binutils.git;a=patch;h=260cd95271cdf002ed8e419898fd29c42e257841")
md5sums=('5d76604f545b151230d1c86e1b8cfab3'
         'ad86b2b889424fd1a3b07e7c54ecf646')

build() {
  [ $NOEXTRACT -eq 1 ] || tar --lzma -xf binutils-$pkgver-${_uprel}-mingw32-src.tar.lzma
  [ $NOEXTRACT -eq 1 ] || tar xjf binutils-$pkgver-${_uprel}-mingw32-src/binutils-$pkgver.tar.bz2

  cd $srcdir/binutils-$pkgver
  patch -Np1 <$srcdir/260cd952.patch || true
  ./configure \
    --target=i486-mingw32 \
    --host=$CHOST \
    --build=$CHOST \
    --prefix=/usr \
    --disable-nls \
    --enable-shared
  make
}

package() {
  cd $srcdir/binutils-$pkgver
  make install DESTDIR=$pkgdir
  rm -rf $pkgdir/usr/lib
  rm -rf $pkgdir/usr/share/{info,man}
}
