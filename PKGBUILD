# Maintainer: Harley Laue <losinggeneration@gmail.com>
pkgname=zerobrane-studio-git
pkgver=2454.7a8027e
pkgrel=1
pkgdesc="A lightweight Lua-based IDE for Lua with code completion, syntax highlighting, live coding, remote debugger, and code analyzer."
arch=(any)
url="http://studio.zerobrane.com/"
license=('MIT')
depends=('wxlua' 'lua51-bitop' 'lua51-socket' 'hicolor-icon-theme')
makedepends=('git' 'cmake')
provides=('zerobrane-studio')
conflicts=('zerobrane-studio')
optdepends=('love: to debug love programs')
install=zerobrane-studio.install
source=(
	"git+https://github.com/pkulchenko/ZeroBraneStudio.git"
	"zbstudio.patch")
md5sums=('SKIP'
	'3bb356b8549b60352e8ab36b9a6d9a92')

pkgver() {
	cd "$srcdir/ZeroBraneStudio"
	echo $(git rev-list --count HEAD).$(git rev-parse --short HEAD)
}

build() {
  cd "$srcdir/ZeroBraneStudio"

  patch -p1 < "$srcdir/zbstudio.patch"

  cd build

  cmake -DCMAKE_INSTALL_PREFIX=/usr \
        -DCMAKE_BUILD_TYPE=RelWithDebInfo \
        -DLUA_EXECUTABLE=/usr/bin/lua5.1
  make
}

package() {
  cd "$srcdir/ZeroBraneStudio/build"

  make DESTDIR="$pkgdir/" install
  install -d "$pkgdir/usr/share/licenses/$pkgname"
  cp ../LICENSE "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
