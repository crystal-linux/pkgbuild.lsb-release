# Arch Maintainer: Jonas Witschel <diabonas@archlinux.org>
# Contributor: Sven-Hendrik Haase <sh@lutzhaase.com>
# Contributor: Malte Rabenseifner <malte@zearan.de>
# Contributor: John Gerritse <reaphsharc@gmail.com>

pkgname=lsb-release
pkgver=2.0.r48.3cf5103
_commit=3cf51039933d03ef15388b75d30baa5d5e09a1a0
pkgrel=2
pkgdesc="LSB version query program"
arch=('any')
url="https://refspecs.linuxfoundation.org/lsb.shtml"
license=('GPL')
depends=('sh')
makedepends=('git')
source=("git+https://github.com/LinuxStandardBase/lsb-samples.git#commit=$_commit"
        'lsb-release'
        'lsb_release_description.patch'
        'lsb_release_make_man_page_reproducible.patch')
sha512sums=('SKIP'
            '105576065947756b92b7d3b6280aa2fcd0d7c91dfd5e03c5dabc4ac457c150421b6c0d5a6ba31ea885008fa4dfe0b6e150acdd279d60c2a75f42baca831493b1'
            'fb5a08408f7e3c6f2b2f04bb3d3a7dc7a23aff16c13b4e8359a814c0234bc13263ba4c9c819e8f5f9721d8f303815de5d1ccc84fbcbdf9cbba1eab279a7be831'
            'cf62c753ba42961136da606505dc53f69bfc1d3d963e982b84fe4cfea68ceef4954965797b95501dff1b17be78c070e927f9fb524c4aa530214a84aba2518ecb')

pkgver() {
	cd lsb-samples/lsb_release/src
	printf "%s.r%s.%s" "$(grep -Po 'SCRIPTVERSION="\K[^"]*' lsb_release)" "$(git rev-list --count HEAD)" "$(git rev-parse --short HEAD)"
}

prepare() {
	cd lsb-samples/lsb_release/src
	patch -Np0 -i "$srcdir/lsb_release_description.patch"
	patch -Np1 -i "$srcdir/lsb_release_make_man_page_reproducible.patch"
}

build() {
	cd lsb-samples/lsb_release/src
	make
}

package() {
	cd lsb-samples/lsb_release/src
	install -Dm644 lsb_release.1.gz -t "$pkgdir/usr/share/man/man1"
	install -Dm755 lsb_release -t "$pkgdir/usr/bin"
	install -Dm644 "$srcdir/lsb-release" -t "$pkgdir/etc"
}
