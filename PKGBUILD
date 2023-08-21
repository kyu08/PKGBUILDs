# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Maintainer: Caleb Maclennan <caleb@alerque.com>

pkgname=editorconfig-checker
pkgver=2.7.1
pkgrel=1
pkgdesc='A tool to verify that your files are in harmony with your .editorconfig'
arch=('x86_64')
url="https://github.com/editorconfig-checker/$pkgname"
license=(MIT)
depends=(glibc)
makedepends=(go)
provides=(ec)
source=("$pkgname-$pkgver.tar.gz::$url/archive/refs/tags/$pkgver.tar.gz")
sha256sums=('3e33229a8c9cb402ce1d4be7bd7ee6119661dd12c69818dfbd579093dec282cd')

build() {
	cd "$pkgname-$pkgver"
	export CGO_CPPFLAGS="$CPPFLAGS"
	export CGO_CFLAGS="$CFLAGS"
	export CGO_CXXFLAGS="$CXXFLAGS"
	export CGO_LDFLAGS="$LDFLAGS"
	export GOFLAGS="-buildmode=pie -trimpath -ldflags=-linkmode=external -mod=readonly -modcacherw"
	go build -o "$pkgname" ./cmd/...
}

check() {
	cd "$pkgname-$pkgver"
	go test ./...
}

package() {
	cd "$pkgname-$pkgver"
	install -Dm755 -t "$pkgdir/usr/bin/" "$pkgname"
	ln -sf "$pkgname" "$pkgdir/usr/bin/ec"
	install -Dm644 -t  "$pkgdir/usr/share/licenses/$pkgname" LICENSE
}

# vim: ts=2 sw=2 et:
