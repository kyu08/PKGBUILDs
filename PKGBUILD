# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sematre <sematre at gmx dot de>

pkgname=cargo-deb
pkgver=1.44.0
pkgrel=1
pkgdesc="Cargo subcommand that generates Debian packages"
arch=('x86_64')
url="https://github.com/kornelski/cargo-deb"
license=('MIT')
depends=('xz')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('86a4ba1e4461a2dd416992fab65908f4f42c29a4ffbc38c482a256790cc1228f')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
}


check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen -- --skip "dependencies::resolve_test"
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
