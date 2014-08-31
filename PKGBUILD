# Maintainer: Jan de Groot <jgc@archlinux.org>
# Maintainer: JIN Xiao-Yong <jinxiaoyong@gmail.com>
# Maintainer: bohoomil <@zoho.com>

pkgname=freetype2-infinality-ultimate
pkgver=2.5.3
pkgrel=11
_patchrel=2014.08.25
pkgdesc="TrueType font rendering library with Infinality patches and custom settings by bohoomil (infinality-bundle)."
arch=('i686' 'x86_64')
changelog=CHANGELOG
license=('GPL' 'MIT')
groups=('infinality-bundle')
url="http://freetype.sourceforge.net"
depends=('zlib' 'bzip2' 'sh' 'xorg-xrdb' 'libpng' 'harfbuzz')
conflicts=('freetype2' 'freetype2-infinality')
provides=("freetype2=$pkgver" 'freetype2-infinality' 'freetype2-infinality-ultimate')
install='infinality.install'
backup=('etc/profile.d/infinality-settings.sh')
source=(http://downloads.sourceforge.net/sourceforge/freetype/freetype-${pkgver}.tar.bz2
        infinality-settings.sh
        freetype-2.5.3-enable-valid.patch
        "upstream-${_patchrel}.patch"
        "infinality-2.5.3-${_patchrel}.patch")
sha1sums=('d3c26cc17ec7fe6c36f4efc02ef92ab6aa3f4b46'
          '42ad32b566cf9d4b91feecb1b421a2ee2176c8fa'
          'abf7a8f726ad6359533651a8942636880febf9f6'
          'd3d04a9e263e1868ac74c634ccd14c027c846b2a'
          '7df648c3188cad78dfafe90ee4687b31c256d1c1')

prepare() {
  cd "freetype-${pkgver}"

  patches=(freetype-2.5.3-enable-valid.patch
           "upstream-${_patchrel}.patch"
           "infinality-2.5.3-${_patchrel}.patch")

  # infinality & post release fixes
  for patch in "${patches[@]}"; do
    patch -Np1 -i ${srcdir}/"${patch}"
  done
}

build() {
  cd "freetype-${pkgver}"

  ./configure \
    --prefix=/usr \
    --disable-static \
    --with-harfbuzz \
    --with-png

  make
}

check() {
  cd "freetype-${pkgver}"
  make -k check
}

package() {
  cd "freetype-${pkgver}"

  make DESTDIR="${pkgdir}" install
  install -D -T "${srcdir}/infinality-settings.sh" \
    "${pkgdir}/etc/profile.d/infinality-settings.sh"
}
