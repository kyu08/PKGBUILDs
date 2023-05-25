# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=gpg-tui
pkgver=0.9.6
pkgrel=1
pkgdesc="A terminal user interface for GnuPG"
arch=('x86_64')
url="https://github.com/orhun/gpg-tui"
license=('MIT')
depends=('libxcb' 'libxkbcommon' 'gpgme')
makedepends=('cargo' 'python')
optdepends=(
  'xplr: for file selection support'
  'xclip: for clipboard support on X11 (or xsel)'
  'xsel: for clipboard support on X11 (or xclip)'
  'wl-clipboard: for clipboard support on Wayland'
)
source=("$pkgname-$pkgver.tar.gz::$url/archive/v$pkgver.tar.gz")
sha512sums=('c4068dd27e861b4a32db40872415988ed634a7e707981e8fc065feea2cef959d5c5f0fefae4f0c7a9d1da45c4ec6589bfae57714c9140a1df7fbac89e6046ae5')

prepare() {
  cd "$pkgname-$pkgver"
  mkdir completions/
  cargo fetch --locked --target "$CARCH-unknown-linux-gnu"
}

build() {
  cd "$pkgname-$pkgver"
  cargo build --release --frozen
  OUT_DIR=completions/ target/release/gpg-tui-completions
}

check() {
  cd "$pkgname-$pkgver"
  cargo test --frozen
}

package() {
  cd "$pkgname-$pkgver"
  install -Dm 755 "target/release/$pkgname" -t "$pkgdir/usr/bin"
  install -Dm 644 README.md -t "$pkgdir/usr/share/doc/$pkgname"
  install -Dm 644 LICENSE -t "$pkgdir/usr/share/licenses/$pkgname"
  install -Dm 644 "man/$pkgname.1" -t "$pkgdir/usr/share/man/man1"
  install -Dm 644 "man/$pkgname.toml.5" -t "$pkgdir/usr/share/man/man5"
  install -Dm 644 "completions/$pkgname.bash" "$pkgdir/usr/share/bash-completion/completions/$pkgname"
  install -Dm 644 "completions/$pkgname.fish" -t "$pkgdir/usr/share/fish/vendor_completions.d"
  install -Dm 644 "completions/_$pkgname" -t "$pkgdir/usr/share/zsh/site-functions"
}

# vim: ts=2 sw=2 et:
