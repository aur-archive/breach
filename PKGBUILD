# Maintainer: Eugenio Ferreira <eugfcl@gmail.com>
# Contribuitor: Alfredo Palhares <masterkorp@masterkorp.net>

pkgname=breach
pkgver=0.3.22
pkgrel=2
pkgdesc="Entirely written in Javascript. Free. Modular. Hackable."
url="http://breach.cc/"

_pkgsubver="alpha.6"
_pkgfullver="${pkgver}-${_pkgsubver}"
_pkgfullname="${pkgname}-v${_pkgfullver}-linux-x64"

arch=('x86_64')
license=('MIT')
provides=('breach')
depends=('alsa-lib' 'gcc-libs-multilib' 'gconf' 'gtk2' 'libxtst' 'nodejs' 'nss' 'python')
source=("https://raw.githubusercontent.com/breach/releases/master/v${_pkgfullver}/breach-v${_pkgfullver}-linux-x64.tar.gz"
        "breach.desktop"
        "breach.png")
md5sums=('462bcca90d1885eb6c63e5c9be37d2f8'
         '9169019f6486d896fdf7043e164c3751'
         '9fcea1351e0e6f0612934f6191f18f66')

prepare() {
  cd "$srcdir/$_pkgfullname"

  # avoid exporting useless variables
  sed -i 's/^export.*//' breach

  # specify installation path
  sed -i 's/^\$SRC_DIR/\/opt\/breach/' breach

  # apply suid patch
  # https://github.com/breach/breach_core/issues/60
  sed -i 'N;s/ \+\\.*/ --disable-setuid-sandbox/' breach 
}

package() {
  cd "$srcdir/$_pkgfullname"

  local _installdir='/opt/breach'
  local _license='__AUTO_UPDATE_BUNDLE__/breach_core/LICENSE'
  
  install -Dm644 "$_license" "$pkgdir/usr/share/licenses/${pkgname}/LICENSE"
  install -Dm644 "$srcdir/breach.desktop" "$pkgdir/usr/share/applications/breach.desktop"
  install -Dm644 "$srcdir/breach.png" "$pkgdir/usr/share/pixmaps/breach.png"

  install -d -m755 "$pkgdir/bin"
  install -d -m755 "$pkgdir/$_installdir"
  install -d -m755 "$pkgdir/usr/lib"

  cp -r * "$pkgdir/$_installdir"

  ln -s "$_installdir/$pkgname" "$pkgdir/bin"
  ln -s "/usr/lib/libudev.so" "$pkgdir/usr/lib/libudev.so.0"
}
