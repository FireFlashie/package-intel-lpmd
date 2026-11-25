# Maintainer: Peter Jung <ptr1337@archlinux.org>
# Contributor: Norbert Preining <norbert@preining.info>

pkgname=intel-lpmd
pkgver=0.1.0.1
pkgrel=1
pkgdesc="Intel Low Power Mode Daemon"
arch=(x86_64)
url="https://github.com/FireFlashie/intel-lpmd"
license=('GPL-2.0-or-later')
install=$pkgname.install
makedepends=(
  git
  gtk-doc
  glib2-devel
  systemd
)
depends=(
  glibc
  glib2
  libxml2
  libnl
  systemd-libs
  polkit
  upower
)
source=(git+${url}.git#tag=v${pkgver})
sha256sums=('a65556aa6461f92af70923b167caeb227deb156ba4f872deae4b8f748ebb3ceb')

prepare() {
	cd "$pkgname"
	# Let makepkg handle manpage compression and avoid running mandb during install.
	sed -i '/^install-data-hook:/,+2d' Makefile.am
	./autogen.sh \
		--prefix=/usr \
		--sysconfdir=/etc \
		--sbindir=/usr/bin \
		--localstatedir=/var \
		--with-dbus-sys-dir=/usr/share/dbus-1/system.d
}

build() {
	cd "$pkgname"
	make
}

package() {
	cd "$pkgname"
	DESTDIR="$pkgdir" make install
	install -Dm 644 -t "${pkgdir}/usr/share/doc/${pkgname}" "$srcdir/${pkgname}"/README.md
	install -Dm 644 -t "${pkgdir}/usr/share/doc/${pkgname}" "$srcdir/${pkgname}"/doc/WLT_proxy.md
}
