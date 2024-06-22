# Maintainer: Ivan Gabaldon <aur[at]inetol.net>
# Contributor: sukanka <su975853527 at gmail.com>

pkgname=tradingview
pkgver=2.7.8
pkgrel=1
pkgdesc='A charting platform for traders and investors'
arch=('x86_64')
url='https://www.tradingview.com/desktop/'
license=('LicenseRef-TradingView')
makedepends=('links'
             'squashfs-tools')
noextract=("$pkgname-$pkgver.snap")
source=("$pkgname-$pkgver.snap::https://api.snapcraft.io/api/v1/snaps/download/nJdITJ6ZJxdvfu8Ch7n5kH5P99ClzBYV_54.snap")
b2sums=('737228bc6b1a78faa146a7783349beb2aba759312901799eb07b360055cd2dba39104425b8860da1f471f6a91379515f9b0489c96d4a8ad410892e067c7fd04c')

prepare() {
    unsquashfs -f -n -q -d "$pkgname-$pkgver/" "$pkgname-$pkgver.snap"
    chmod 755 "$pkgname-$pkgver/"

    # License
    links -width 80 -dump 'https://www.tradingview.com/policies/' | sed -n '/Terms of Use/,/TradingView may update these Rules at any time/p' > "LICENSE.txt"

    # Convert
    cd "$pkgname-$pkgver/"

    mv "meta/gui/$pkgname.desktop" "$pkgname.desktop"
    sed -i -e "s|Exec=.*|Exec=/usr/bin/$pkgname %U|" -e "s|Icon=.*|Icon=$pkgname|" "$pkgname.desktop"

    mv "meta/gui/icon.png" "$pkgname.png"

    rm -rf {data-dir/,gnome-platform/,lib/,meta/,scripts/,usr/,*.sh}
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

    install -d "$pkgdir/opt/$pkgname/"
    cp -a "$pkgname-$pkgver/." "$pkgdir/opt/$pkgname/"

    chmod 755 "$pkgdir/opt/$pkgname/$pkgname"

    install -d "$pkgdir/usr/bin/"
    ln -s "/opt/$pkgname/$pkgname" "$pkgdir/usr/bin/$pkgname"

    install -d "$pkgdir/usr/share/applications/"
    ln -s "/opt/$pkgname/$pkgname.desktop" "$pkgdir/usr/share/applications/$pkgname.desktop"

    install -d "$pkgdir/usr/share/icons/hicolor/512x512/apps/"
    ln -s "/opt/$pkgname/$pkgname.png" "$pkgdir/usr/share/icons/hicolor/512x512/apps/$pkgname.png"

    install -Dm644 "LICENSE.txt" -t "$pkgdir/usr/share/licenses/$pkgname/"
}
