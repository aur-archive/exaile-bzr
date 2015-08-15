# Contributor: Alessio Sergi <asergi at archlinux dot us>
# Contributor: Aren Olson <reacocard at gmail dot com>
# Maintainer: Stefan Husmann <stefan-husmann@t-online.de>   

pkgname=exaile-bzr
_pkgname=exaile
pkgver=4367
pkgrel=2
pkgdesc="A full featured music player written for GTK+"
arch=('any')
url="https://launchpad.net/exaile"
license=('GPL2' 'GPL3')
depends=('dbus-python' 'desktop-file-utils' 'gstreamer0.10-good-plugins' \
         'gstreamer0.10-python' 'mutagen' 'pygtk' 'python2-bsddb')
makedepends=('bzr' 'help2man')
optdepends=('exfalso: ex-falso tag editor'
            'gstreamer0.10-plugins: more codecs'
            'ipython: ipython plugin'
            'libgpod: iPod support'
            'moodbar: moodbar plugin'
            'notify-osd: notify-osd notifications'
            'pybonjour: DAAP server plugin'
            'pycddb: CD metadata retrieval'
            'python-notify: libnotify notifications'
            'python-imaging: contextinfo plugin'
            'python2-mmkeys: xkeys plugin'
            'pywebkitgtk: contextinfo plugin'
            'streamripper: streamripper plugin'
            'udisks: device autodetection'
	    'python2-beautifulsoup3: for the Lyrics Wiki plugin')
provides=($_pkgname)
conflicts=($_pkgname $_pkgname-beta $_pkgname-old)
install=$pkgname.install
md5sums=('SKIP')
source="exaile::bzr+http://bazaar.launchpad.net/~exaile-devel/exaile/trunk/"
_bzrmod=exaile

pkgver() {
  cd $srcdir/
  bzr version-info $_bzrmod --custom --template="{revno}\n"
}

build() {
  cd "$srcdir/$_bzrmod"

  # python2 fix
  find plugins/*{,/*}/*.py | xargs sed -i 's_^#.*python$_#!/usr/bin/python2_'

  make
}

package() {
  cd "$srcdir/$_bzrmod"

  make PREFIX=/usr DESTDIR="$pkgdir/" install

  # reference to $pkgdir fix
  sed -i "s|Exec=$pkgdir/*|Exec=/|" "$pkgdir"/usr/share/dbus-1/services/org.exaile.Exaile.service
}
