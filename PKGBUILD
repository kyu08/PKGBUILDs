# Maintainer: Maxime Gauduin <alucryd@archlinux.org>
# Maintainer: Orhun Parmaksız <orhun@archlinux.org>

pkgname=cargo-tarpaulin
pkgver=0.27.0
pkgrel=1
pkgdesc='Tool to analyse test coverage of cargo projects'
arch=(x86_64)
url=https://github.com/xd009642/tarpaulin
license=(Apache MIT)
depends=(
  gcc-libs
  glibc
  libcurl.so
  openssl
  libssh2
  libgit2
  zlib
)
makedepends=(
  git
  rust
)
_tag=2b79e6c966f632b612995f032f9b16dc94aa85c7
source=(git+https://github.com/xd009642/tarpaulin.git#tag=${_tag})
b2sums=('SKIP')

prepare() {
  cargo fetch \
    --locked \
    --target $CARCH-unknown-linux-gnu \
    --manifest-path tarpaulin/Cargo.toml
}

build() {
  export CARGO_TARGET_DIR=target
  export LIBSSH2_SYS_USE_PKG_CONFIG=1
  CFLAGS+=" -ffat-lto-objects"
  cargo build \
    --release \
    --frozen \
    --manifest-path tarpaulin/Cargo.toml
}

package() {
  cd tarpaulin
  install -Dm 755 "${srcdir}/target/release/${pkgname}" -t "${pkgdir}"/usr/bin/
  install -Dm 644 README.md -t "${pkgdir}/usr/share/doc/${pkgname}"
  install -Dm 644 LICENSE-MIT -t "${pkgdir}/usr/share/licenses/${pkgname}"
}

# vim: ts=2 sw=2 et:
