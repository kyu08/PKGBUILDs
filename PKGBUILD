# Maintainer: Orhun Parmaksız <orhun@archlinux.org>
# Contributor: Arne Beer <privat@arne.beer>

pkgname=pueue
pkgver=3.2.0
pkgrel=1
pkgdesc="A CLI tool for managing long running shell commands"
arch=('x86_64')
url="https://github.com/nukesor/pueue"
license=('MIT')
depends=('gcc-libs')
makedepends=('cargo')
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha256sums=('0c3126579661f894fb02a0d8c0e138ab23b277e97cea2d85e48d3d2b9fb1c372')

prepare() {
  cd "$pkgname-$pkgver"
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
  mkdir -p utils/completions/
}

build() {
  cd "$pkgname-$pkgver"
  CFLAGS+=" -ffat-lto-objects"
  cargo build --release --frozen
  ./target/release/pueue completions bash utils/completions/
  ./target/release/pueue completions fish utils/completions/
  ./target/release/pueue completions zsh utils/completions/
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"

  # Install binaries
  install -Dm755 "target/release/pueue" "$pkgdir/usr/bin/pueue"
  install -Dm755 "target/release/pueued" "$pkgdir/usr/bin/pueued"

  # Place systemd user service
  install -Dm644 "utils/pueued.service" "$pkgdir/usr/lib/systemd/user/pueued.service"

  # Install shell completions file
  install -Dm644 "utils/completions/_pueue" "$pkgdir/usr/share/zsh/site-functions/_pueue"
  install -Dm644 "utils/completions/pueue.bash" "$pkgdir/usr/share/bash-completion/completions/pueue.bash"
  install -Dm644 "utils/completions/pueue.fish" "$pkgdir/usr/share/fish/completions/pueue.fish"

  # Install License
  install -Dm644 "LICENSE" "$pkgdir/usr/share/licenses/pueue/LICENSE"
}

# vim: ts=2 sw=2 et:
