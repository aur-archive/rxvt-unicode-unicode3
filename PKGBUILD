# Maintainer: Nicolas Estibals <Nicolas.Estibals@gmail.com>
# Contributor: Angel Velasquez <angvp@archlinux.org>
# Contributor: tobias <tobias@archlinux.org>
# Contributor: dibblethewrecker dibblethewrecker.at.jiwe.dot.org

pkgname=rxvt-unicode-unicode3
_pkgname=rxvt-unicode
pkgver=9.18
pkgrel=1
pkgdesc="An unicode enabled rxvt-clone terminal emulator (urxvt) compiled with --enable-unicode3"
arch=('i686' 'x86_64')
url="http://software.schmorp.de/pkg/rxvt-unicode.html"
license=('GPL')
depends=('gcc-libs' 'libxft' 'gdk-pixbuf2' 'perl')
optdepends=('gtk2-perl: to use the urxvt-tabbed')
provides=('rxvt-unicode')
conflicts=('rxvt-unicode')
source=(http://dist.schmorp.de/rxvt-unicode/${_pkgname}-${pkgver}.tar.bz2 \
        ${_pkgname}.desktop)
sha1sums=('5d12639c4b17019357ee62c08916b826e5d03259'
          '962aebc88982dbeb62a7c4a051ff567e015f61a0')

build() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  ./configure --prefix=/usr \
    --with-terminfo=/usr/share/terminfo \
    --enable-256-color \
    --enable-font-styles \
    --enable-xim \
    --enable-keepscrolling \
    --enable-selectionscrolling \
    --enable-smart-resize \
    --enable-pixbuf \
    --enable-transparency \
    --enable-utmp \
    --enable-wtmp \
    --enable-lastlog \
    --enable-unicode3 \
    --disable-frills
  make
}

package() {
  cd "${srcdir}/${_pkgname}-${pkgver}"
  install -d "${pkgdir}/usr/share/terminfo"
  export TERMINFO="${pkgdir}/usr/share/terminfo"
  make DESTDIR="${pkgdir}" install
 # install the tabbing wrapper ( requires gtk2-perl! )
  sed -i 's/\"rxvt\"/"urxvt"/' doc/rxvt-tabbed
  install -Dm 755 doc/rxvt-tabbed "${pkgdir}/usr/bin/urxvt-tabbed"
 # install freedesktop menu
  install -Dm644 ../${_pkgname}.desktop \
    "${pkgdir}/usr/share/applications/${_pkgname}.desktop"
}
