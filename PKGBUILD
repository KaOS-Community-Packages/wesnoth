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
sha256sums=('70404764370db05e496a4e033e09c26cdc47fa6558271d803a44c4ebb7b6efe8'
'ccacb1049a71935392b46f919c4045b11936b232522ed2763561fbc0fb1e40b7'
'1ae908f0608e9600088d3175c2276923e7fdccf825850d3f6e607bc197987e70'
'd314dbefc72d09f2e3b1db15c4dc20873771f26df2360b39b55481deaeba00db')
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