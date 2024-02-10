# Maintainer: Philip Müller <philm[at]manjaro[dot]org>
# Maintainer: Bernhard Landauer <bernhard[at]manjaro[dot]org>
# Maintainer: Mark Wagie <mark at manjaro dot org>
# Contributor: Helmut Stult
# Contributor: Levente Polyak <anthraxx[at]archlinux[dot]org>
# Contributor: Morten Linderud <foxboron@archlinux.org>

pkgname=pacman
pkgver=6.0.2
pkgrel=18
pkgdesc="A library-based package manager with dependency support"
arch=('x86_64')
url="https://www.archlinux.org/pacman/"
license=('GPL-2.0-or-later')
depends=('bash' 'glibc' 'libarchive' 'curl' 'gpgme' 'pacman-mirrorlist'
         'gettext' 'gawk' 'coreutils' 'gnupg' 'grep')
makedepends=('meson' 'asciidoc' 'doxygen')
checkdepends=('python' 'fakechroot')
optdepends=('perl-locale-gettext: translation support in makepkg-template')
provides=('libalpm.so')
backup=(etc/pacman.conf
        etc/makepkg.conf)
options=('strip')
validpgpkeys=('6645B0A8C7005E78DB1D7864F99FFE0FEAE999BD'  # Allan McRae <allan@archlinux.org>
              'B8151B117037781095514CA7BBDFFC92306B1121') # Andrew Gregory (pacman) <andrew@archlinux.org>
source=(https://sources.archlinux.org/other/pacman/$pkgname-$pkgver.tar.xz{,.sig}
        pacman-always-create-directories-from-debugedit.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/efd0c24c07b86be014a4edb5a8ece021b87e3900.patch
        pacman-always-create-directories-from-debugedit-fixup.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/86981383a2f4380bda26311831be94cdc743649b.patch
        pacman-fix-unique-source-paths.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/478af273dfe24ded197ec54ae977ddc3719d74a0.patch
        pacman-strip-include-o-files-similar-to-kernel-modules.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/de11824527ec4e2561e161ac40a5714ec943543c.patch
        pacman-fix-compatibility-with-bash-5.2-patsub_replacement.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/0e938f188692c710be36f9dd9ea7b94381aed1b4.patch
        pacman-fix-order-of-fakechroot-fakeroot-nesting.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/05f283b5ad8f5b8f995076e93a27c8772076f872.patch
        pacman-change-default-checksum-from-md5-to-sha256.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/aa3a1bc3b50d797fb75278f79a83cd7dde50c66e.patch
        pacman-sort-debuginfod-repro.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/843bf21e794c79c5b3bcf8a57e45ef9c62312fee.patch
        pacman-split-off-strip-debug.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/7a4fff3310ba2eadd3d5428cbb92e58eb2ee853b.patch 
        pacman-ignore-a-files.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/00d2b1f90261bf77eaaf262d2504af016562f2ac.patch
        pacman-early-err-git.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/3aa096a74f717d31650e0eb3cf34e9a5ebadc313.patch
        pacman-fix-gnupg-binary-data.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/86ec26b2d33372a4b3bda48f22c4a9f226c3ccce.patch
        pacman-fix-gnupg-newsig-check.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/16a064701a30d7e1175e1185cc6da44238302fab.patch
        pacman-check-pipes-gnupg.patch::https://gitlab.archlinux.org/pacman/pacman/-/commit/f8c2e59ec57c86827b1f1b1c2f6760dc3e59fe40.patch
        pacman.conf
        makepkg.conf
        pacman-sync-first-option.patch)
sha256sums=('7d8e3e8c5121aec0965df71f59bedf46052c6cf14f96365c4411ec3de0a4c1a5'
            'SKIP'
            '522b789e442b3bb3afa7ea3fa417a99554f36ec00de3986cbe92c80f09a7db99'
            'dab7c70fb9d77d702069bb57f5a12496b463d68ae20460fb0a3ffcb4791321a9'
            '0b56c61eac3d9425d68faa2eccbaefdc5ed422b643974ae829eaca0460043da1'
            'acd0b149b6324dc1eca3cd2d3b30df6ef64c5653e83523d77200ec593e01d2a7'
            '8641d514ef4cae9e4d1867aadf4b9c850a9e8dc9792c6c559f9d2a0e1713a5a1'
            'b11f62d4bd9557e9d3e7456bc95f63e9eabab5ecee1368f4a14a84bc94b1c8d1'
            'cf749ad981e8f3dedd89c05a5e69a9c91d1e58ef9407e8f8e04ba9c183939623'
            '17e7af22533984924aaf1cf36c74aa26b46b04ad140cd76b65521be906bd3ff7'
            '94d1f3575d0c3faf8bf11fee8e5ef36c8b339ebfd24868931903ba179ffecf4e'
            '96efb79a96abf8cdcecb9f8dc461552549cf46159f44bb4160eb073e1ea5000a'
            '0ac6a34e6fc126a243a642e509f459f6cde20af213ab949791a5cc325cf031f9'
            '6e81b34e6a5f312d48ce3aaca0f02ddd10b7a43325cb32acf7666b6b7ac41552'
            '250598a27a3077ec1dfe97a30af8bb0daf449d3ab456ed6a0c7a5bea0eb58f51'
            '94c273f07e4e28125b6002567c62e1f6c65f543597de6a8bd79e8c5bf6e4a125'
            '69dbd2197423fe8be9ec74cb9fa58a819996abc5d19b4569fe84fc9c076397b7'
            '1af9e9bd27d326ccd334f12d601b532b6fab902c1c46a4932b9c44e8c8b60711'
            '8167155d3a3e15fc4a1b1e989fdb826779e7b3690a52e2ca9d307ae0b1550e1d')

prepare() {
  cd "${pkgname}-${pkgver}"
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
}

check() {
  cd "$pkgname-$pkgver"

  meson test -C build
}

package() {
  cd "$pkgname-$pkgver"

  DESTDIR="$pkgdir" meson install -C build

  # install Arch specific stuff
  install -dm755 "$pkgdir/etc"
  install -m644 "$srcdir/pacman.conf" "$pkgdir/etc"
  install -m644 "$srcdir/makepkg.conf" "$pkgdir/etc"

  local wantsdir="$pkgdir/usr/lib/systemd/system/sockets.target.wants"
  install -dm755 "$wantsdir"

  local unit
  for unit in dirmngr gpg-agent gpg-agent-{browser,extra,ssh} keyboxd; do
    ln -s "../${unit}@.socket" "$wantsdir/${unit}@etc-pacman.d-gnupg.socket"
  done
}

# vim: set ts=2 sw=2 et:

