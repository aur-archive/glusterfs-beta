# Maintainer : Kaushal M <kshlmster at gmail dot com>

_basename=glusterfs
_basever=3.4
pkgname=$_basename-beta
pkgver=$_basever.0beta4
pkgrel=2
pkgdesc="A cluster filesystem capable of scaling to several petabytes"
arch=(x86_64)
options=(debug)
provides=(glusterfs)
conflicts=(glusterfs glusterfs-git)
url="http://www.gluster.org"
license=(GPL2 LGPL3)
depends=('fuse' 'libxml2' 'python2' 'libaio' 'lvm2' 'openssl' 'libibverbs' 'ncurses' 'readline')
source=(http://bits.gluster.org/pub/gluster/glusterfs/src/glusterfs-${pkgver}.tar.gz
        glusterd.service)

sha256sums=('7a832bda141c06bda4cf83afa6aa1026efc0c95544ff6f4eaf8b191569c66b05'
            'ab573a99f89df686bdd0a02539cfb342e8157a16952706efa8fa60a2f88795fe')

build() {
        cd $srcdir/$_basename-$pkgver

        ./configure \
                --prefix=/usr \
                --sysconfdir=/etc  \
                --localstatedir=/var \
                --mandir=/usr/share/man \
                --libexecdir=/usr/lib/$_basename \
                --sbindir=/usr/bin \
                --with-mountutildir=/usr/bin \
                PYTHON=python2

        make
}

package() {
        cd $srcdir/$_basename-$pkgver

        make -j1 DESTDIR=$pkgdir install

        install -D -m 644 README \
                $pkgdir/usr/share/doc/glusterfs/
        install -D -m 644 INSTALL \
                $pkgdir/usr/share/doc/glusterfs/
        install -D -m 644 COPYING-* \
                $pkgdir/usr/share/doc/glusterfs/

        install -D -m 644 $srcdir/glusterd.service \
                $pkgdir/usr/lib/systemd/system/glusterd.service
}
