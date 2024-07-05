# Maintainer: Ivan Gabaldon <aur[at]inetol.net>
# Contributor: sukanka <su975853527 at gmail.com>

pkgname=tradingview
_pkgname=TradingView
pkgver=2.8.0
pkgrel=2
pkgdesc='A charting platform for traders and investors'
arch=('x86_64')
url='https://www.tradingview.com/desktop/'
license=('LicenseRef-TradingView')
makedepends=('links')
source=("$pkgname-$pkgver.deb::https://tvd-packages.tradingview.com/ubuntu/stable/pool/multiverse/t/tradingview/jammy/$pkgname-$pkgver-1_amd64.deb")
b2sums=('f967621b5dcb596909e9b298a1748d0a71a9e054d697bfe8cbb2760c748614b3a125d281e4d35f2f5df1dd52e6acfb91e32a67e2e58a8b7b13d9f9779ce52df2')

prepare() {
    mkdir -p "$pkgname-$pkgver/"
    bsdtar -xpf 'data.tar.xz' -C "$pkgname-$pkgver/"

    # Convert
    cd "$pkgname-$pkgver/"

    links -width 80 -dump 'https://www.tradingview.com/policies/' | sed -n '/Terms of Use/,/TradingView may update these Rules at any time/p' > "opt/$_pkgname/LICENSE"

    mv "usr/share/applications/$pkgname.desktop" "opt/$_pkgname/$pkgname.desktop"
    sed -i -e "s|Exec=.*|Exec=/usr/bin/$pkgname %U|" "opt/$_pkgname/$pkgname.desktop"

    mv "usr/share/icons/hicolor/512x512/apps/$pkgname.png" "opt/$_pkgname/$pkgname.png"
}

package() {
    depends=('alsa-lib'
             'at-spi2-core'
             'cairo'
             'dbus'
             'expat'
             'gcc-libs'
             'glib2'
             'glibc'
             'gtk3'
             'hicolor-icon-theme'
             'libcups'
             'libdrm'
             'libsecret'
             'libx11'
             'libxcb'
             'libxcomposite'
             'libxdamage'
             'libxext'
             'libxfixes'
             'libxkbcommon'
             'libxrandr'
             'mesa'
             'nspr'
             'nss'
             'pango')

    optdepends=('libappindicator-gtk3: Systray indicator support'
                'xdg-utils: Open files')

    install -d "$pkgdir/opt/$pkgname/"
    cp -a "$pkgname-$pkgver/opt/$_pkgname/." "$pkgdir/opt/$pkgname/"

    chmod 755 "$pkgdir/opt/$pkgname/$pkgname"

    install -d "$pkgdir/usr/bin/"
    ln -s "/opt/$pkgname/$pkgname" "$pkgdir/usr/bin/$pkgname"

    install -d "$pkgdir/usr/share/applications/"
    ln -s "/opt/$pkgname/$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"

    install -d "$pkgdir/usr/share/icons/hicolor/512x512/apps/"
    ln -s "/opt/$pkgname/$pkgname.png" "$pkgdir/usr/share/icons/hicolor/512x512/apps/$pkgname.png"

    install -d "$pkgdir/usr/share/licenses/$pkgname/"
    ln -s "/opt/$pkgname/LICENSE" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
