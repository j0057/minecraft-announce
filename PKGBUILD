# Maintainer: Joost Molenaar <jjm@j0057.nl>

pkgname=mcannounce

pkgver=0.1
pkgrel=1

arch=(any)

pkgdesc='Dynamically manages Minecraft LAN port in firewall'
url="https://github.com/j0057/minecraft-announce"
license=(MIT)

depends=(
    jq
    python
)
optdepends=(
    'nftables: for nftables support using mcannounce-nft'
)

source=(mcannounce
        mcannounce-nft
        mcannounce-nft.service
        README.md
        LICENSE)

sha256sums=(SKIP
            SKIP
            SKIP
            SKIP
            SKIP)

package() {
    install -o root -g root -m 755 -d $pkgdir/usr/bin
    install -o root -g root -m 755 -t $pkgdir/usr/bin mcannounce
    install -o root -g root -m 755 -t $pkgdir/usr/bin mcannounce-nft

    install -o root -g root -m 755 -d $pkgdir/usr/lib/systemd/system
    install -o root -g root -m 644 -t $pkgdir/usr/lib/systemd/system mcannounce-nft.service

    install -o root -g root -m 755 -d $pkgdir/usr/share/doc/$pkgname
    install -o root -g root -m 644 -t $pkgdir/usr/share/doc/$pkgname README.md

    install -o root -g root -m 755 -d $pkgdir/usr/share/licenses/$pkgname
    install -o root -g root -m 644 -t $pkgdir/usr/share/licenses/$pkgname LICENSE
}
