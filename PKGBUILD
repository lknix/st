pkgname=st-lknix
pkgver=0.7
pkgrel=1
pkgdesc='A simple virtual terminal emulator for X with personalized config'
arch=('i686' 'x86_64')
license=('MIT')
depends=('libxft' 'libxext' 'xorg-fonts-misc')
makedepends=('ncurses')
conflicts=('st', 'st-git')
url="http://st.suckless.org"
source=(http://dl.suckless.org/st/st-$pkgver.tar.gz
        config.h)
md5sums=('29b2a599cf1511c8062ed8f025c84c63'
         '4dcf9ba6c60d6a93584faa64837d6fd3')

prepare() {
  cd $srcdir/st-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/\@tic /d' Makefile
  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/st-$pkgver
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/st-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/st/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/st/README"
}
