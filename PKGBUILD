# Maintainer: Somebody <somebody[at]foo[dot]tld>
pkgname=eventlircd
pkgver=0.0.1+svn20110409.0930
pkgrel=0
pkgdesc="Eventlircd daemon"
url="http://code.google.com/p/eventlircd/"
arch=('x86_64' 'i686')
license=('GPLv2')
depends=('automake')
optdepends=()
makedepends=()
conflicts=()
replaces=()
backup=()
#install=()
source=("https://launchpad.net/~yavdr/+archive/main/+files/eventlircd_0.0.1%2Bsvn20110409.0930.orig.tar.gz"
        "eventlircd.service")
 
md5sums=('c5c126946bb40e8a7f0c033af87e7334'
         '42612a870047e245723b9c0efd0e0044')

build() {
  cd "${srcdir}/${pkgname}-${pkgver}"

  sed -i 's/\s\-Werror//' configure.ac
  sed -i 's/AM_CONFIG_HEADER/AC_CONFIG_HEADER/' configure.ac
  autoreconf -vfi
  sed -i 's/\/sbin/\/bin/g' configure
  ./configure \
        --prefix=/usr \
        --sysconfdir=/etc \
        --disable-dependency-tracking \
        --with-lircd-socket=/var/run/lirc/lircd \
        --with-evmap-dir=/etc/eventlircd.d \
        --with-udev-dir=/usr/lib/udev
  sed -i 's/\/sbin/\/bin/' Makefile
  make
}

package() {
  cd "${srcdir}/${pkgname}-${pkgver}"
  make DESTDIR="${pkgdir}" install
  install -Dm644 COPYING "$pkgdir/usr/share/licenses/$pkgname/COPYING"
  install -Dm644 "${srcdir}/eventlircd.service" "$pkgdir/usr/lib/systemd/system/eventlircd.service"
}

 
# vim:set ts=2 sw=2 et:
