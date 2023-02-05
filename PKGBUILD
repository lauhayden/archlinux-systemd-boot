# Maintainer: Hayden Lau <arch@hlau.ca>
# Development at https://github.com/lauhayden/archlinux-systemd-boot
pkgname=archlinux-systemd-boot
pkgver='2023.02.01'
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
  '39b9cdf671f9958db73188bd06c25397b7354dedc171152d8fe639ec315d48defe9ffd64d870beab479c13d0d0d28c4e8039542c8ec2f4d0e5fcc342b73eb000'
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
