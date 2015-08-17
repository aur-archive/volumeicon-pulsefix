# Maintainer: Alejandro Perez <alejandro.perez.mendez@gmail.com>

pkgname=volumeicon-pulsefix
pkgver=20140305_1
pkgrel=1
pkgdesc="Volume control for your system tray - Some fixes for pulseaudio"
arch=('x86_64' 'i686')
url="http://softwarebakery.com/maato/volumeicon.html"
license=('GPL3')
depends=('gtk3' 'alsa-lib' 'libnotify' 'intltool')

conflicts=('volumeicon' 'volumeicon-git')
replaces=('volumeicon')
makedepends=('git')
provides=('volumeicon')


_gitroot="git://github.com/Maato/volumeicon.git"
_gitname="volumeicon"

source=(volumeicon-pulseaudio-fix.patch)
md5sums=('16ea0c3870e1495a872d9f318637779b')

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [ -d $_gitname ] ; then
    cd $_gitname && git pull origin
    msg "The local files are updated."
  else
    git clone $_gitroot $_gitname
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"

  cd "$srcdir/$_gitname-build"

  patch -Np1 -i ../volumeicon-pulseaudio-fix.patch

  ./autogen.sh
  ./configure --prefix=/usr --enable-notify
  make
}

package() {
  cd "$srcdir/$_gitname-build"

  make DESTDIR="$pkgdir/" install
}
