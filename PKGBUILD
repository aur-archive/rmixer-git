# Maintainer: Mattias Andrée <`base64 -d`(bWFhbmRyZWUK)@member.fsf.org>
pkgname=rmixer-git
pkgver=20130809
pkgrel=1
pkgdesc="Simple remote interface for the ALSA mixer"
arch=('any')
url="https://github.com/maandree/rmixer"
license=('WTFPL')
depends=('java-runtime>=7' 'alsa-util')
makedepends=('git' 'java-environment>=7' 'texinfo' 'gzip' 'auto-auto-complete')
provides=('rmixer')
conflicts=('rmixer')

_gitroot=https://github.com/maandree/rmixer.git
_gitname=rmixer

build() {
  cd "$srcdir"
  msg "Connecting to GIT server...."

  if [[ -d "$_gitname" ]]; then
    cd "$_gitname" && git pull origin
    msg "The local files are updated."
  else
    git clone "$_gitroot" "$_gitname"
  fi

  msg "GIT checkout done or server timeout"
  msg "Starting build..."

  rm -rf "$srcdir/$_gitname-build"
  git clone "$srcdir/$_gitname" "$srcdir/$_gitname-build"
  cd "$srcdir/$_gitname-build"

  make DESTDIR="$pkgdir/"
}

package() {
  cd "$srcdir/$_gitname-build"
  make DESTDIR="$pkgdir/" install
}
