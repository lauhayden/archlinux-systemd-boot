# Maintainer: Hayden Lau <arch@hlau.ca>
# Development at https://github.com/lauhayden/archlinux-systemd-boot
pkgname=archlinux-systemd-boot
pkgver='2023.05.03'
pkgrel=1
pkgdesc='Arch Install Media as systemd-boot loader entry'
url='https://archlinux.org/download/'
arch=('x86_64')
license=('various')
depends=('systemd')

source=(
  "https://geo.mirror.pkgbuild.com/iso/${pkgver}/archlinux-${pkgver}-x86_64.iso"
  "https://geo.mirror.pkgbuild.com/iso/${pkgver}/archlinux-${pkgver}-x86_64.iso.sig"
  'arch-installmedia.conf'
)
noextract=("archlinux-${pkgver}-x86_64.iso")
validpgpkeys=('3E80CA1A8B89F69CBA57D98A76A5EF9054449A5C')
b2sums=(
  '6d8f1ae992900cb10cdd3e1abd6137d59ce08e3cc532f9fd67dd629058b4404488a854ce5baa56c7c516c386f0296d7768e964f660bdd53c66d5f1ecf3268938'
  'SKIP'
  'SKIP'
)

prepare() {
  cd "${srcdir}"
  bsdtar xf archlinux-${pkgver}-x86_64.iso shellx64.efi
  bsdtar xf archlinux-${pkgver}-x86_64.iso arch
  # fix permissions
  chmod 755 shellx64.efi
  chmod -R 755 arch
}

check() {
  # ensure that the ESP is labled 'ESP'
  [[ $(findmnt -n -o LABEL -T /boot) == 'ESP' ]]
}

package() {
  install -d "${pkgdir}"/boot/loader/entries
  cp arch-installmedia.conf "${pkgdir}"/boot/loader/entries
  cp "${srcdir}"/shellx64.efi "${pkgdir}"/boot
  install -d "${pkgdir}"/boot/arch-installmedia
  cp -r "${srcdir}"/arch/* "${pkgdir}"/boot/arch-installmedia
}
