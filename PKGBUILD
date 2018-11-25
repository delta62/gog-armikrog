# Maintainer: Sam Noedel <sam.noedel@gmail.com>
pkgname=gog-armikrog
pkgver=2.5.0.6
pkgrel=2
pkgdesc="Armikrog is a unique stop motion clay animated point and click adventure game from the creators of Earthworm Jim and the Neverhood"
url="https://www.gog.com/game/armikrog"
license=('custom')
arch=('any')
depends=()
makedepends=()
checkdepends=()
optdepends=()
options=()
install=
changelog=
source=(
  "${pkgname}_${pkgver}.sh"
  "$pkgname.desktop")
noextract=()
md5sums=(
  "4ca9ac6d05ac66c18229e41da6fd89dd"
  "429f12d83ee7eac085a4ecf7c48c969a")

prepare() {
  unzip "${pkgname}_${pkgver}.sh" || :
  cd "$srcdir/data/noarch"
  sed -r -i \
    's/(CURRENT_DIR="\$\( cd "\$\( dirname )'`
      `'"\$\{BASH_SOURCE\[0\]\}"(.*$)'`
      `'/\1$( readlink -nf "${BASH_SOURCE[0]}" )\2/' \
  "start.sh"
}

package() {
  cd "$srcdir/data/noarch"

  install -d "$pkgdir/opt/$pkgname/"
  install -d "$pkgdir/opt/$pkgname/support"
  install -d "$pkgdir/usr/bin/"

  cp -r "game/" "$pkgdir/opt/$pkgname"

  install -Dm755 "start.sh" "$pkgdir/opt/$pkgname/"
  install -Dm755 support/*.sh{,lib} -t "$pkgdir/opt/$pkgname/support"

  # Desktop integration
  install -Dm644 "support/icon.png" "$pkgdir/usr/share/pixmaps/$pkgname.png"
  install -Dm644 "docs/End User License Agreement.txt" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
  install -Dm644 "$srcdir/$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"
  ln -s "/opt/$pkgname/start.sh" "$pkgdir/usr/bin/$pkgname"
}
