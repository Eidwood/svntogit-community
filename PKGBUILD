# Maintainer: Daniel Micay <danielmicay@gmail.com>
# Contributor: hauzer <hauzer at gmx dot com>
_hkgname=hashable
pkgname=haskell-hashable
pkgver=1.2.1.0
pkgrel=1
pkgdesc="A class for types that can be converted to a hash value"
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:BSD3')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' haskell-text)
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
md5sums=('74f7cadb836e63f4d4b1a24be401228d')

build() {
  cd "${srcdir}/${_hkgname}-${pkgver}"
  runhaskell Setup configure -O ${PKGBUILD_HASKELL_ENABLE_PROFILING:+-p } --enable-split-objs --enable-shared \
    --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
  runhaskell Setup build
  runhaskell Setup haddock
  runhaskell Setup register   --gen-script
  runhaskell Setup unregister --gen-script
  sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}

package() {
  cd "${srcdir}/${_hkgname}-${pkgver}"
  install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
  install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
  install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
  ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
  runhaskell Setup copy --destdir=${pkgdir}
  install -D -m644 LICENSE ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
  rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
