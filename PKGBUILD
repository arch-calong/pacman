# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult
# Contributor: Jonas Strassel <info[at]jonas-strassel[dot]de>

# Arch credits:
# Dan McGee <dan@archlinux.org>
# Dave Reisner <dreisner@archlinux.org>

pkgname=pacman
pkgver=6.0.2
_pkgver=1.8.2
pkgrel=8
pkgdesc="A library-based package manager with dependency support"
arch=('x86_64')
url="https://www.archlinux.org/pacman/"
license=('GPL')
groups=('base-devel')
depends=('bash' 'glibc' 'libarchive' 'curl' 'gpgme'
         'gettext' 'gawk' 'coreutils' 'gnupg' 'grep'
         'fakeroot' 'perl' # pacman-contrib deps
         'pacman-mirrors')
makedepends=('meson' 'asciidoc' 'doxygen')
checkdepends=('python' 'fakechroot')
optdepends=('perl-locale-gettext: translation support in makepkg-template'
            'diffutils: for pacdiff'
            'findutils: for pacdiff --find'
            'mlocate: for pacdiff --locate'
            'sudo: privilege elevation for several scripts'
            'vim: default merge program for pacdiff'
            'haveged: for pacman-init.service')
provides=('pacman-contrib' 'pacman-init' 'libalpm.so')
conflicts=('pacman-contrib' 'pacman-init')
replaces=('pacman-contrib' 'pacman-init')
backup=(etc/pacman.conf
        etc/makepkg.conf)
install=pacman.install
validpgpkeys=('6645B0A8C7005E78DB1D7864F99FFE0FEAE999BD' # Allan McRae <allan@archlinux.org>
              'B8151B117037781095514CA7BBDFFC92306B1121' # Andrew Gregory (pacman) <andrew@archlinux.org>
              '04DC3FB1445FECA813C27EFAEA4F7B321A906AD9') # Daniel M. Capella <polyzen@archlinux.org>
#              '5134EF9EAF65F95B6BB1608E50FB9B273A9D0BB5') # Johannes Löthberg <johannes@kyriasis.com>

source=(https://sources.archlinux.org/other/pacman/$pkgname-$pkgver.tar.xz{,.sig}
        https://gitlab.archlinux.org/pacman/pacman-contrib/-/archive/v$_pkgver/pacman-contrib-v$_pkgver.tar.gz
        pacman-always-create-directories-from-debugedit.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/efd0c24c07b86be014a4edb5a8ece021b87e3900.patch
        pacman-always-create-directories-from-debugedit-fixup.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/86981383a2f4380bda26311831be94cdc743649b.patch
        pacman-fix-unique-source-paths.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/478af273dfe24ded197ec54ae977ddc3719d74a0.patch
        pacman-strip-include-o-files-similar-to-kernel-modules.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/de11824527ec4e2561e161ac40a5714ec943543c.patch
        pacman.conf
        makepkg.conf
        pacman-sync-first-option.patch
        etc-pacman.d-gnupg.mount
        pacman-init.service
        10-example.pre.repo.conf
        10-example.post.repo.conf)
sha256sums=('7d8e3e8c5121aec0965df71f59bedf46052c6cf14f96365c4411ec3de0a4c1a5'
            'SKIP'
            '4a00142292df4297ce19e58156bffd8235084cdc2dd3db22b58a5577243242c0'
            '522b789e442b3bb3afa7ea3fa417a99554f36ec00de3986cbe92c80f09a7db99'
            'dab7c70fb9d77d702069bb57f5a12496b463d68ae20460fb0a3ffcb4791321a9'
            '0b56c61eac3d9425d68faa2eccbaefdc5ed422b643974ae829eaca0460043da1'
            'acd0b149b6324dc1eca3cd2d3b30df6ef64c5653e83523d77200ec593e01d2a7'
            'f924d4bfee9cc00aa45cf04e56769e52a9dff7b0889d933ccdca9dfece671a8b'
            '40c8c0f874a3ce1e2290be95f79b772e1e3661b7e99608e1742349eb192c0f5a'
            '8167155d3a3e15fc4a1b1e989fdb826779e7b3690a52e2ca9d307ae0b1550e1d'
            'b6d14727ec465bb66d0a0358163b1bbfafcb4eaed55a0f57c30aabafae7eed68'
            '65d8bdccdcccb64ae05160b5d1e7f3e45e1887baf89dda36c1bd44c62442f91b'
            'a978a8ca7b1573309cdcc9d33c328e760dbe62bdba71841c66579e9f84fff182'
            'ea3fb1c6427f4e3668ff4c28b211c3837746c99cfe0c2ae1e7d7502b1aaec607')

prepare() {
  cd $pkgname-$pkgver
  # we backport way too often in pacman
  # lets at least make it more convenient
  local src
  for src in "${source[@]}"; do
    src="${src%%::*}"
    src="${src##*/}"
    [[ $src = *.patch ]] || continue
    msg2 "Applying patch $src..."
    patch -Np1 < "../$src"
  done

  cd $srcdir/pacman-contrib-v$_pkgver
  ./autogen.sh
}

build() {
  cd "$pkgname-$pkgver"

  meson --prefix=/usr \
        --buildtype=plain \
        -Ddoc=enabled \
        -Ddoxygen=enabled \
        -Dscriptlet-shell=/usr/bin/bash \
        -Dldconfig=/usr/bin/ldconfig \
        build

  meson compile -C build

  cd $srcdir/pacman-contrib-v$_pkgver

  ./configure \
    --prefix=/usr \
    --sysconfdir=/etc \
    --localstatedir=/var
  make
}

check() {
  cd "$pkgname-$pkgver"
  meson test -C build

  make -C ../pacman-contrib-v$_pkgver check
}

package() {
  cd "$pkgname-$pkgver"

  DESTDIR="$pkgdir" meson install -C build

  # install Arch specific stuff
  install -dm755 "$pkgdir/etc"
  install -m644 "$srcdir/pacman.conf" "$pkgdir/etc"
  install -m644 "$srcdir/makepkg.conf" "$pkgdir/etc"

  # install pacman-init
  install -dm755 $pkgdir/usr/lib/systemd/system/
  install -m644 $srcdir/etc-pacman.d-gnupg.mount $pkgdir/usr/lib/systemd/system/etc-pacman.d-gnupg.mount
  install -m644 $srcdir/pacman-init.service $pkgdir/usr/lib/systemd/system/pacman-init.service

  cd $srcdir/pacman-contrib-v$_pkgver

  make DESTDIR="$pkgdir" install

  # replace rankmirrors
  rm "$pkgdir/usr/bin/rankmirrors"
  ln -sfv "/usr/bin/pacman-mirrors" "$pkgdir/usr/bin/rankmirrors"

  # add pre/post repo configuration
  install -dm755 "$pkgdir/etc/pacman.d"
  install -m644 "$srcdir/10-example.pre.repo.conf" "$pkgdir/etc/pacman.d"
  install -m644 "$srcdir/10-example.post.repo.conf" "$pkgdir/etc/pacman.d"
}
