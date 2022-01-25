# Maintainer: Matt C <mdc028[at]bucknell[dot]edu>
# Contributor: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Malte Rabenseifner <malte@zearan.de>
# Contributor: John Gerritse <reaphsharc@gmail.com>

pkgname=lsb-release
pkgver=1.4
pkgrel=24
pkgdesc="LSB version query program"
arch=('any')
url="http://www.linuxbase.org/"
license=('GPL2')
depends=('bash')
install=lsb-release.install
source=(https://downloads.sourceforge.net/lsb/$pkgname-$pkgver.tar.gz
        lsb_release_description.patch
        lsb_release_make_man_page_reproducible.patch)
sha512sums=('84f6f8794380463587005043f601b7a40190cd9e3409abff7f5ce7658cf029a14346eff87838296d90307192bdeff68cc00480c5c04814da7acdb3e220640fde'
            'fb5a08408f7e3c6f2b2f04bb3d3a7dc7a23aff16c13b4e8359a814c0234bc13263ba4c9c819e8f5f9721d8f303815de5d1ccc84fbcbdf9cbba1eab279a7be831'
            'cf62c753ba42961136da606505dc53f69bfc1d3d963e982b84fe4cfea68ceef4954965797b95501dff1b17be78c070e927f9fb524c4aa530214a84aba2518ecb')

prepare() {
  cd "$srcdir/$pkgname-$pkgver"

  patch -Np0 < "$srcdir/lsb_release_description.patch"
  patch -Np1 < "$srcdir/lsb_release_make_man_page_reproducible.patch"
}


build() {
  cd "$srcdir/$pkgname-$pkgver"

  make
}

package() {
  cd "$srcdir/$pkgname-$pkgver"

  install -dm755 "$pkgdir/etc"
  echo "LSB_VERSION=$pkgver" >> "$pkgdir/etc/lsb-release"
  echo "DISTRIB_ID=\"Crystal Linux\"" >> "$pkgdir/etc/lsb-release"
  echo "DISTRIB_RELEASE=rolling" >> "$pkgdir/etc/lsb-release"
  echo "DISTRIB_DESCRIPTION=\"Crystal Linux\"" >> "$pkgdir/etc/lsb-release"

  install -Dm 644 lsb_release.1.gz "$pkgdir/usr/share/man/man1/lsb_release.1.gz"
  install -Dm 755 lsb_release "$pkgdir/usr/bin/lsb_release"
}
