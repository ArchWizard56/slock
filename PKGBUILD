# Maintainer: Archwizard <archwizard101@gmail.com>
pkgname=slock
pkgver=1.4
pkgrel=3
pkgdesc="A simple screen locker for X"
arch=('x86_64')
url="http://tools.suckless.org/slock"
license=('MIT')
depends=('libxext' 'libxrandr')
source=("http://dl.suckless.org/tools/$pkgname-$pkgver.tar.gz" "https://tools.suckless.org/slock/patches/dpms/slock-dpms-20170923-fa11589.diff" "https://tools.suckless.org/slock/patches/message/slock-message-20180626-35633d4.diff"  "config.diff")
#source=("slock-$pkgver.tar.bz2::http://hg.suckless.org/slock/archive/$_pkgver.tar.gz")
md5sums=('f91dd5ba50ce7bd1842caeca067086a3'
         '2afeace988ef4eaf0a8a078aded7c4a0'
         'c6f6136ef2dc3765644a7dd2fed6f53e'
         'a0be01d5d6876481a77a0345150594e9')


prepare() {
  cd "$srcdir/slock-$pkgver"
  sed -i 's|static const char \*group = "nogroup";|static const char *group = "nobody";|' config.def.h
  sed -ri 's/((CPP|C|LD)FLAGS) =/\1 +=/g' config.mk
  patch -p1< ../slock-message-20180626-35633d4.diff
  patch -F 3 -p1 < ../slock-dpms-20170923-fa11589.diff
  patch < ../config.diff
  sed -i 's/text_size = "6x10"/text_size = "6x13"/g' config.def.h
}

build() {
  cd "$srcdir/slock-$pkgver"
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd "$srcdir/slock-$pkgver"
  make PREFIX=/usr DESTDIR="$pkgdir" install
  install -m644 -D LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
