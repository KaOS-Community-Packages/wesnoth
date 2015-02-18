 pkgname=wesnoth
pkgver=1.12.1
pkgrel=1
pkgdesc="A turn-based strategy game on a fantasy world."
arch=('x86_64')
license=('GPL2')
url="http://www.wesnoth.org/"
depends=('boost-libs' 'freetype2' 'fribidi' 'gcc-libs' 'icu' 'libvorbis' 'lua' 'pango' 'sdl_image' 'sdl_mixer'
'sdl_net' 'sdl_ttf' 'dbus' 'python2')
makedepends=('boost' 'cmake')
categories=('games')
source=(http://downloads.sourceforge.net/sourceforge/${pkgname}/${pkgname}-${pkgver}.tar.bz2
"wesnoth-boost.patch"
"wesnothd.tmpfiles.conf"
"wesnothd.service")
md5sums=('SKIP'
 '2f77149a722823517be50e22b1511758'
 '348136e6136294295daefcec771203e9'
 'c26cd0c5ee303fc46556deb6a2400d18')
build() {
cd ${srcdir}/${pkgname}-${pkgver}
# Try this again in a new version when they fix their linking to boost
patch -Np1 < ${srcdir}/wesnoth-boost.patch
mkdir -p build && cd build
cmake \
-DCMAKE_INSTALL_PREFIX=/usr \
-DENABLE_CAMPAIGN_SERVER=ON \
-DENABLE_TOOLS=ON \
-DENABLE_OMP=ON \
-DCMAKE_BUILD_TYPE=RelWithDebugInfo \
..
make
}
package() {
cd ${srcdir}/${pkgname}-${pkgver}/build
make DESTDIR=$pkgdir install
install -Dm644 "$srcdir/wesnothd.tmpfiles.conf" "$pkgdir/usr/lib/tmpfiles.d/wesnothd.conf"
install -Dm644 "$srcdir/wesnothd.service" "$pkgdir/usr/lib/systemd/system/wesnothd.service"
}