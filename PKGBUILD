# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Vlad Frolov <frolvlad@gmail.com>

pkgname=cargo-udeps
pkgver=0.1.42
pkgrel=1
pkgdesc="Find unused dependencies in Cargo.toml"
arch=('x86_64')
url="https://github.com/est31/cargo-udeps"
license=('MIT' 'Apache')
depends=('curl' 'libgit2')
makedepends=('cargo' 'libssh2')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('b89c4ba44112a5b9d544bc8555a69f2fa24f44a0a389035cd38f19827a262e78')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  export LIBSSH2_SYS_USE_PKG_CONFIG=1
  CFLAGS+=" -ffat-lto-objects"
  cargo build --release --frozen
}

# Tests require rustup nightly
#check() {
#  cd "$pkgname-$pkgver"
#  cargo test --release --locked
#}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
}

# vim:set ts=2 sw=2 et:
