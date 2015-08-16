# $Id$
# Maintainer: Balló György <ballogyor+arch at gmail dot com>
# Contributor: Jason Graham <jason@the-graham.com>
# Contributor: Thomas Baechler <thomas@archlinux.org>
# Contributor: James Rayner <iphitus@gmail.com>

_pkgbasename=nvidia-173xx-utils
pkgname=lib32-$_pkgbasename
pkgver=173.14.39
pkgrel=3
pkgdesc="NVIDIA drivers utilities and libraries, 173xx branch. (32-bit)"
arch=('x86_64')
ARCH=x86
url="http://www.nvidia.com/"
depends=('lib32-libxvmc' 'lib32-zlib' 'lib32-gcc-libs' 'nvidia-173xx-utils' 'lib32-mesa')
conflicts=('lib32-mesa-libgl' 'lib32-catalyst-utils' 'lib32-nvidia-utils' 'lib32-nvidia-304xx-utils')
provides=('lib32-libgl')
license=('custom')
options=('!strip')
source=("http://us.download.nvidia.com/XFree86/Linux-${ARCH}/${pkgver}/NVIDIA-Linux-${ARCH}-${pkgver}-pkg0.run")
md5sums=('5b423543428554ef33a200fbbe3cb9fc')

package() {
	cd $srcdir
	sh NVIDIA-Linux-${ARCH}-${pkgver}-pkg0.run --extract-only
	cd NVIDIA-Linux-${ARCH}-${pkgver}-pkg0/usr/

	mkdir -p $pkgdir/usr/lib32
	mkdir -p $pkgdir/usr/share/licenses/

	install lib/{libGLcore,libGL,libnvidia-cfg,tls/libnvidia-tls}.so.${pkgver} \
	$pkgdir/usr/lib32/
	install X11R6/lib/libXv* $pkgdir/usr/lib32/
	cd $pkgdir/usr/lib32/
	ln -s libGL.so.$pkgver libGL.so
	ln -s libGL.so.$pkgver libGL.so.1
	ln -s libGLcore.so.$pkgver libGLcore.so.1
	ln -s libnvidia-cfg.so.$pkgver libnvidia-cfg.so.1
	ln -s libnvidia-tls.so.$pkgver libnvidia-tls.so.1
	ln -s libXvMCNVIDIA.so.$pkgver libXvMCNVIDIA_dynamic.so.1

	# We have to provide symlinks to mesa, as nvidia 173xx doesn't ship them
	ln -s mesa/libEGL.so.1.0.0 "${pkgdir}/usr/lib32/libEGL.so.1.0.0"
	ln -s libEGL.so.1.0.0      "${pkgdir}/usr/lib32/libEGL.so.1"
	ln -s libEGL.so.1.0.0      "${pkgdir}/usr/lib32/libEGL.so"

	ln -s mesa/libGLESv1_CM.so.1.1.0 "${pkgdir}/usr/lib32/libGLESv1_CM.so.1.1.0"
	ln -s libGLESv1_CM.so.1.1.0      "${pkgdir}/usr/lib32/libGLESv1_CM.so.1"
	ln -s libGLESv1_CM.so.1.1.0      "${pkgdir}/usr/lib32/libGLESv1_CM.so"

	ln -s mesa/libGLESv2.so.2.0.0 "${pkgdir}/usr/lib32/libGLESv2.so.2.0.0"
	ln -s libGLESv2.so.2.0.0      "${pkgdir}/usr/lib32/libGLESv2.so.2"
	ln -s libGLESv2.so.2.0.0      "${pkgdir}/usr/lib32/libGLESv2.so"

	ln -s nvidia-173xx $pkgdir/usr/share/licenses/lib32-nvidia-173xx-utils

	find $pkgdir/usr -type d -exec chmod 755 {} \;
}
