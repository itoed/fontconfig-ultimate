# Maintainer: Jan de Groot <jgc@archlinux.org>
# Maintainer: JIN Xiao-Yong <jinxiaoyong@gmail.com>
# Maintainer: bohoomil <@zoho.com>

pkgname=freetype2-infinality-ultimate
pkgver=2.5.3
pkgrel=10
_patchrel=2014.08.08
pkgdesc="TrueType font rendering library with Infinality patches and custom settings by bohoomil (infinality-bundle)."
arch=('i686' 'x86_64')
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
          '2bceadc3283de4dbedcf18a95ef4e75d4212cc35'
          'abf7a8f726ad6359533651a8942636880febf9f6'
          '6cf9c5ef2ade7f2460d19d12b072a73b48958ac9'
          'a9c16046836b13a67a1158b87669f7f18ffe1665')

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
  install -D -T "${srcdir}/infinality-settings.sh" "${pkgdir}/etc/profile.d/infinality-settings.sh"
}