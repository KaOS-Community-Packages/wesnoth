pkgname=wesnoth
pkgver=1.12.1
pkgrel=1
pkgdesc="A turn-based strategy game on a fantasy world"
arch=('x86_64')
license=('GPL')
url="http://www.wesnoth.org/"
depends=('sdl1_ttf' 'sdl_net' 'sdl_mixer' 'sdl_image' 'fribidi' 'boost-libs' 'pango' 'lua' 'wesnoth-data' 'dbus' 'python2')
makedepends=('boost' 'cmake'' git')
install=wesnoth.install
options=(!emptydirs)
source=("git://github.com/wesnoth/wesnoth.git#tag=${pkgver}"
        "wesnoth-boost.patch"
        wesnothd.tmpfiles.conf
        wesnothd.service)
md5sums=('SKIP'
         '2f77149a722823517be50e22b1511758'
         '348136e6136294295daefcec771203e9'
         'c26cd0c5ee303fc46556deb6a2400d18')

build() {
  cd "$srcdir/$pkgname"
  
  # Try this again in a new version when they fix their linking to boost
  patch -Np1 < ${srcdir}/wesnoth-boost.patch

  mkdir build && cd build
  cmake .. \
      -DCMAKE_INSTALL_PREFIX=/usr \
      -DENABLE_OMP=ON \
      -DENABLE_TOOLS=ON \
      -DMANDIR=share/man
  make
}

package() {
  cd "$srcdir/$pkgname"

  cd build
  make DESTDIR="$pkgdir" install

  rm -r $pkgdir/usr/share/applications
  rm -r $pkgdir/usr/share/doc
  rm -r $pkgdir/usr/share/pixmaps
  rm -r $pkgdir/usr/share/wesnoth

  install -Dm644 "$srcdir/wesnothd.tmpfiles.conf" "$pkgdir/usr/lib/tmpfiles.d/wesnothd.conf"
  install -Dm644 "$srcdir/wesnothd.service" "$pkgdir/usr/lib/systemd/system/wesnothd.service"
} 
