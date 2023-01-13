# Maintainer: Hayden Lau <arch@hlau.ca>
pkgname=archlinux-systemd-boot
pkgver="2023.01.01"
pkgrel=1
pkgdesc="Arch Install Media as systemd-boot loader entry"
url=""
arch=(any)
license=(GPL)
depends=(systemd)

source=(
	https://geo.mirror.pkgbuild.com/iso/$pkgver/archlinux-x86_64.iso
	arch-installmedia.conf
)
noextract=(archlinux-x86_64.iso)
sha256sums=(
  "61dbae312cf677be38a93f424c91abadd8a8ed1f3a602b697aac4c57a7872645"
  "SKIP"
)

prepare() {
  cd $srcdir
  bsdtar xf archlinux-x86_64.iso shellx64.efi
  bsdtar xf archlinux-x86_64.iso arch
  # fix permissions
  chmod 755 shellx64.efi
  chmod -R 755 arch
}

package() {
  install -d $pkgdir/boot/loader/entries
  cp arch-installmedia.conf $pkgdir/boot/loader/entries
  cp $srcdir/shellx64.efi $pkgdir/boot
  cp -r $srcdir/arch $pkgdir/boot
}
