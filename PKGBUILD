# Maintainer: Arch Haskell Team <arch-haskell@haskell.org>
_hkgname=happstack-helpers
pkgname=haskell-happstack-helpers
pkgver=0.52
pkgrel=3
pkgdesc="Convenience functions for Happstack."
url="http://hackage.haskell.org/package/${_hkgname}"
license=('custom:BSD3')
arch=('i686' 'x86_64')
makedepends=()
depends=('ghc' 'haskell-debugtracehelpers' 'haskell-hstringtemplate<0.7.0' 'haskell-hstringtemplatehelpers>=0.0.14' 'haskell-http=4000.0.9' 'haskell-missingh>=1.0.3' 'haskell-pbkdf2<0.4' 'haskell-bytestring=0.9.1.7' 'haskell-containers=0.3.0.0' 'haskell-directory=1.0.1.1' 'haskell-filepath=1.1.0.4' 'haskell-happstack-data<0.6' 'haskell-happstack-ixset<0.6' 'haskell-happstack-server<0.6' 'haskell-happstack-state<0.6' 'haskell-haskell98=1.0.1.1' 'hscolour<1.14' 'haskell-mtl<2.0.0.0' 'haskell-network=2.2.1.7' 'haskell-old-time=1.0.0.5' 'haskell-parsec=2.1.0.1' 'haskell-puremd5<1.1.0.0' 'haskell-random=1.0.0.2' 'haskell-safe<0.3' 'haskell-syb=0.1.0.2' 'haskell-text<0.11' 'haskell-utf8-string<0.4.0')
options=('strip')
source=(http://hackage.haskell.org/packages/archive/${_hkgname}/${pkgver}/${_hkgname}-${pkgver}.tar.gz)
install=${pkgname}.install
build() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    runhaskell Setup configure -O --enable-split-objs --enable-shared \
       --prefix=/usr --docdir=/usr/share/doc/${pkgname} --libsubdir=\$compiler/site-local/\$pkgid
    runhaskell Setup build
    runhaskell Setup haddock
    runhaskell Setup register   --gen-script
    runhaskell Setup unregister --gen-script
    sed -i -r -e "s|ghc-pkg.*unregister[^ ]* |&'--force' |" unregister.sh
}
package() {
    cd ${srcdir}/${_hkgname}-${pkgver}
    install -D -m744 register.sh   ${pkgdir}/usr/share/haskell/${pkgname}/register.sh
    install    -m744 unregister.sh ${pkgdir}/usr/share/haskell/${pkgname}/unregister.sh
    install -d -m755 ${pkgdir}/usr/share/doc/ghc/html/libraries
    ln -s /usr/share/doc/${pkgname}/html ${pkgdir}/usr/share/doc/ghc/html/libraries/${_hkgname}
    runhaskell Setup copy --destdir=${pkgdir}
    install -D -m644 bsd3.txt ${pkgdir}/usr/share/licenses/${pkgname}/LICENSE
    rm -f ${pkgdir}/usr/share/doc/${pkgname}/LICENSE
}
md5sums=('892c69f011c8e04ad206035c287f3b28')
