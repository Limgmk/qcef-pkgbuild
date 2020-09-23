# Maintainer: Limgmk <limgmkgm@gmail.com>

pkgname=qcef
pkgver=1.1.8
pkgrel=1
pkgdesc="Qt5 binding of CEF"
arch=('x86_64')
url="https://github.com/linuxdeepin/qcef"
license=('GPL')
depends=('gconf' 'gtk2' 'libxss' 'nss' 'libpulse' 'qt5-webchannel' 'qt5-x11extras')
makedepends=('cmake' 'qt5-tools')
_cef_binary_commit=fecf00339545d2819224333cc506d5aa22ae8008
source=("$pkgname-$pkgver.tar.gz::https://github.com/linuxdeepin/qcef/archive/$pkgver.tar.gz"
		"cef-binary-${_cef_binary_commit}.zip::https://github.com/linuxdeepin/cef-binary/archive/${_cef_binary_commit}.zip"
		"CMakeLists.txt.patch"
		"cef_variables.cmake.patch")
sha512sums=('72a3a0ca4ef655407e583469f2d55ac38bd6e829e8f9ee270df794a724f192667a97796cb9825a8b08c82810d486091cd504d0387561a3a08615a1e0b2cdfcbd'
		'310adbaef333a54c56b9b49af653b6d5c4b00952bf44036b561e4c7544af547332f758bc73d0531f51494b8e0701f6b4900bbe7dac36faca7009009c7800dd1f'
		'34a3d83abc573d13fd11c85aa85b0ec7dfb9117b297395773996d38f9cda3314561ccbbecbe0312ebe70dfb641a66c124c3d5e9afbdf40ba0487db5cad9bc406'
		'acb7eb990a1a76d7fe10ec962590efb22989b68544a2722de684080ffede8b52af54de706f4126e9baac18f95fcef696eb3ac4bc2cc9ef6ef4a8d45d4941e278')

prepare() {
	rm -rf qcef-$pkgver/cef
	mv cef-binary-${_cef_binary_commit} qcef-$pkgver/cef
	patch qcef-$pkgver/src/CMakeLists.txt < CMakeLists.txt.patch
	patch qcef-$pkgver/cef/cmake/cef_variables.cmake < cef_variables.cmake.patch
	mkdir -p build
}

build() {
	cd build
	cmake -DCMAKE_INSTALL_PREFIX=/usr -DCMAKE_BUILD_TYPE=Release ../qcef-$pkgver
	make -j12
}

package() {
	cd build
	make DESTDIR="$pkgdir" install
}
