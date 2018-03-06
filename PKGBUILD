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
        config.h
        https://st.suckless.org/patches/scrollback/st-scrollback-$pkgver.diff
        https://st.suckless.org/patches/hidecursor/st-hidecursor-$pkgver.diff
       )

_patches=(st-scrollback-$pkgver.diff
          st-hidecursor-$pkgver.diff
         )

md5sums=('29b2a599cf1511c8062ed8f025c84c63'
         'f6e339677c0af811e66571fa4de96b6f'
         'c55076d94247e121a1a86d32a793cf2e'
         '8ff8a77b34dfc09a4dd0d2cf876d68e7')

prepare() {
  cd $srcdir/st-$pkgver
  # skip terminfo which conflicts with nsurses
  sed -i '/\@tic /d' Makefile
  cp $srcdir/config.h config.h
}

build() {
  cd $srcdir/st-$pkgver
  for patch in "${_patches[@]}"; do
    echo "Applying patch $patch..."
    patch -Np1 -i "$srcdir/$patch"
  done
  make X11INC=/usr/include/X11 X11LIB=/usr/lib/X11
}

package() {
  cd $srcdir/st-$pkgver
  make PREFIX=/usr DESTDIR="$pkgdir" TERMINFO="$pkgdir/usr/share/terminfo" install
  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/st/LICENSE"
  install -Dm644 README "$pkgdir/usr/share/doc/st/README"
}
