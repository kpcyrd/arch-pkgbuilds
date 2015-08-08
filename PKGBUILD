# Maintainer: Sebastian Lau <archlinux _at_ slau _dot_ info>
# Maintainer: Eric Ozwigh <ozwigh at gmail dot com>

pkgname=veracrypt
_pkgname=VeraCrypt
pkgver=1.12
_pkgver=${pkgver//_/-}
pkgrel=1
pkgdesc="Disk encryption with strong security based on TrueCrypt"
arch=('i686' 'x86_64')
url="http://veracrypt.codeplex.com/"
license=('custom')
depends=('fuse' 'wxgtk>=3.0.0' 'libsm' 'device-mapper')
makedepends=('nasm')
install='veracrypt.install'
source=("https://github.com/${pkgname}/${_pkgname}/archive/${_pkgname}_${pkgver}.tar.gz"
	"no_makeself.patch"
        "veracrypt.desktop"
        "veracrypt.install")
sha1sums=('43cf537c334a0aeffb66a2e14b092a27b5a51eba'
          '0cbe9f7875ab52be125cc575533f76fab60314a5'
          'ebdd450e719fe3cff5e459f027856cbaf03db13a'
          '2d4bec531ba3f053abd806aff83bd72f1baedadb')

build() {
  cd ${srcdir}/${_pkgname}-${_pkgname}_${pkgver}/src

  msg2 "Applying patch..."
  patch -Np1 -i ../../no_makeself.patch  # disable sfx archive
  # build
  export WX_CONFIG=/usr/bin/wx-config
  make LFLAGS+="-ldl"
}

package() {
  cd ${srcdir}/${_pkgname}-${_pkgname}_${pkgver}/src
  install -D -m755 Main/${pkgname} "${pkgdir}/usr/bin/${pkgname}"
  install -D -m644 "${srcdir}/${pkgname}.desktop" "${pkgdir}/usr/share/applications/${pkgname}.desktop"
  install -D -m644 Resources/Icons/VeraCrypt-48x48.xpm "${pkgdir}/usr/share/pixmaps/veracrypt.xpm"
  install -D -m644 License.txt "${pkgdir}/usr/share/licenses/${pkgname}/License.txt"
}
