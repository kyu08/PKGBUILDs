# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Sanpi <sanpi+aur@homecomputing.fr>

pkgname=grcov
pkgver=0.8.19
pkgrel=1
pkgdesc="Rust tool to collect and aggregate code coverage data for multiple source files"
arch=('x86_64')
url="https://github.com/mozilla/grcov"
license=('MPL2')
depends=('zlib' 'gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('d8ea0fb293dc5431b502e8ffbd7c9a62336d9e878df9b78a8aed57098fbfb2d8')

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
  cargo test --frozen --lib
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
}

# vim: ts=2 sw=2 et:
