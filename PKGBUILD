# Maintainer: Trustin Lee <t@motd.kr>
# Maintainer: Sabart Otto - Seberm <seberm@gmail.com>

pkgname=dnrd-svn
pkgver=250
pkgrel=2
pkgdesc="Domain Name Relay Daemon is a caching, forwarding DNS proxy server."
arch=('i686' 'x86_64') 
url="http://dnrd.sourceforge.net"
license=('GPL')
conflicts=('dnrd')
makedepends=('subversion')
source=('svn+http://svn.code.sf.net/p/dnrd/code/trunk'
        'case_insensitive_match.patch')
sha1sums=('SKIP'
          'd7078421c34a1da861cf6ec874b8b5a6558dfb3c')
install='dnrd.install'

pkgver() {
  cd trunk/dnrd
  svnversion
}

prepare() {
  cd trunk/dnrd
  patch -p2 < ../../case_insensitive_match.patch
  mv configure.in configure.ac
  aclocal
  autoheader
  automake -a
  autoconf
}

build() {
  cd trunk/dnrd
  ./configure --prefix=/usr --sysconfdir=/etc --enable-tcp
  make
}

package() {
  cd trunk/dnrd
  make DESTDIR="$pkgdir" install
  mkdir -p $pkgdir/usr/bin
  mv $pkgdir/usr/sbin/* $pkgdir/usr/bin
  rmdir $pkgdir/usr/sbin
  mkdir -p $pkgdir/etc/dnrd
  chmod 755 $pkgdir/etc/dnrd
}

