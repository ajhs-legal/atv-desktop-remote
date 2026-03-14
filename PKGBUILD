pkgname=atv-desktop-remote
pkgver=2.1.1
pkgrel=1
pkgdesc="Control an Apple TV from your desktop"
arch=('x86_64')
url="https://github.com/ajhs-legal/atv-desktop-remote"
license=('MIT')
depends=('alsa-lib' 'at-spi2-core' 'gtk3' 'libnotify' 'nss' 'libxss')
makedepends=('nodejs' 'npm')
options=('!strip')

build() {
  cd "$startdir"
  npm install --legacy-peer-deps
  npx electron-builder --linux dir --publish never
}

package() {
  cd "$startdir"

  install -dm755 "$pkgdir/opt/atv-desktop-remote"
  cp -a dist/linux-unpacked/. "$pkgdir/opt/atv-desktop-remote/"

  install -dm755 "$pkgdir/usr/bin"
  ln -s /opt/atv-desktop-remote/atv-desktop-remote "$pkgdir/usr/bin/atv-desktop-remote"

  install -Dm644 build/icon.png "$pkgdir/usr/share/pixmaps/atv-desktop-remote.png"

  install -dm755 "$pkgdir/usr/share/applications"
  cat <<'EOF' > "$pkgdir/usr/share/applications/atv-desktop-remote.desktop"
[Desktop Entry]
Type=Application
Name=ATV Remote
Comment=Control an Apple TV from your desktop
Exec=/usr/bin/atv-desktop-remote
Icon=atv-desktop-remote
Categories=Utility;
Terminal=false
EOF

  install -Dm644 LICENSE "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
}
