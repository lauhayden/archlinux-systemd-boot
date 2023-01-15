# Maintainer: Hayden Lau <arch@hlau.ca>
# Development at https://github.com/lauhayden/archlinux-systemd-boot
pkgname=archlinux-systemd-boot
pkgver=2023.01.01
pkgrel=4
pkgdesc='Arch Install Media as systemd-boot loader entry'
url='https://archlinux.org/download/'
arch=('x86_64')
license=('various')
depends=('systemd')

source=(
  'https://geo.mirror.pkgbuild.com/iso/$pkgver/archlinux-x86_64.iso'
  'https://geo.mirror.pkgbuild.com/iso/$pkgver/archlinux-x86_64.iso.sig'
  'arch-installmedia.conf'
)
noextract=('archlinux-x86_64.iso')
validpgpkeys=('3E80CA1A8B89F69CBA57D98A76A5EF9054449A5C')
b2sums=(
  '664a0328a81c7d4efc4bce0019c1845809cb10ac9a3235ef6a51647c65a2ab1ec6c8f61f817b67dabb62660e2958931c06ffbe25e27c10def3844a5b5a304dcf'
  'SKIP'
  'SKIP'
)

prepare() {
  cd $srcdir
  bsdtar xf archlinux-x86_64.iso shellx64.efi
  bsdtar xf archlinux-x86_64.iso arch
  # fix permissions
  chmod 755 shellx64.efi
  chmod -R 755 arch
}

check() {
  # ensure that the ESP is labled 'ESP'
  [[ $(findmnt -n -o LABEL -T /boot) == 'ESP' ]]
}

package() {
  install -d $pkgdir/boot/loader/entries
  cp arch-installmedia.conf $pkgdir/boot/loader/entries
  cp $srcdir/shellx64.efi $pkgdir/boot
  install -d $pkgdir/boot/arch-installmedia
  cp -r $srcdir/arch/* $pkgdir/boot/arch-installmedia
}
