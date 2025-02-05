# Install DEB packages on Archlinux

example-package.deb

## Create a PKGBUILD using vim

```bash
vim PKGBUILD
```

## Paste the following into the PKGBUILD file

```vim
# PKGBUILD
# Metadata; be sure to set this to reasonable values to not confuse your
# package manager or cause name conflicts with the repositories.
pkgname="package"
pkgver="0.0.1"
pkgrel="1"
pkgdesc="package"
arch=("x86_64")

# The RPM file you want to install; place in the same directory as this file.
source=("example-package.deb")

# Assuming you're not going to push this to AUR or whatever, you can just skip
# the integrity check here. Otherwise, replace SKIP with the output of
# "sha -a 256 example-package.deb".
sha256sums=("SKIP")

package() {
  # Copy all directories from $srcdir into $pkgdir. $srcdir will already have
  # been populated with the contents of example-package.deb, but it also contains a
  # symlink to it, which we don't want to copy; anything in $pkgdir after this
  # command will be installed to your root directory.
  find $srcdir/ -mindepth 1 -maxdepth 1 -type d | xargs cp -r -t "$pkgdir"
}
```

## Exit vim and make the zst package using makepkg

```bash
makepkg
```

## Install the custom package using pacman

```bash
sudo pacman -U ./example-package.pkg.tar.zst
```
