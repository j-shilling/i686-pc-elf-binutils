# Maintainer: Jake Shilling <shilling.jake@gmail.com>

_target=i686-pc-elf
pkgname=$_target-binutils
pkgver=2.31
pkgrel=1
pkgdesc='The GNU Binutils are a collection of binary tools for the i686-pc-elf target'
arch=(i686 x86_64)
url='http://www.gnu.org/software/bintuils/'
license=(GPL)
depends=(zlib)
options=(!emptydirs !docs)
source=("http://mirrors.kernel.org/gnu/binutils/binutils-$pkgver.tar.xz")
md5sums=('ddbb923470fcf59c8c4d08a9e9a79cf9')
_basedir=binutils-$pkgver

prepare() {
	cd $_basedir
	if [[ -e $srcdir/binutils-build ]]; then
		rm -Rf $srcdir/binutils-build
	fi
	mkdir $srcdir/binutils-build
}

build() {
	cd binutils-build

	CPPFLAGS=${CPPFLAGS//-D_FORTIFY_SOURCE=?/}
	export CPPFLAGS

	$srcdir/$_basedir/configure \
		--target=$_target \
		--with-sysroot \
		--prefix=/usr/ \
		--disable-nls \
		--disable-werror

	make
}

check() {
	cd binutils-build

	make -k check
}

package() {
	cd binutils-build

	make DESTDIR="$pkgdir" install
	rm -Rf ${pkgdir}/usr/share
}
