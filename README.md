# aur

Own PKGBUILDs — packages the AUR has in the wrong flavour or not at all.
One directory per package, with the `.SRCINFO` makepkg generates.

## Packages

- `tokyonight-gtk-theme-storm-git` — the Tokyo Night GTK theme built for
  the Storm variant only (`--tweaks storm`, dark, default accent) plus the
  Tokyonight-Dark icons. The AUR's `tokyonight-gtk-theme-git` builds the
  installer's defaults, which is the Night palette. Installs
  `/usr/share/themes/Tokyonight-Dark-Storm` and
  `/usr/share/icons/Tokyonight-Dark`; the dotfiles name both in `[gtk]`
  of `.chezmoidata.toml`.

## Using

Build and install one with yay, which pulls the dependencies from the
repositories and the AUR and installs makedepends (sassc for the theme)
on the way. `-B` alone only builds and leaves the package next to the
PKGBUILD; `-i` installs it too:

    yay -Bi ~/src/personal/aur/<package>

The dotfiles' fish has `aur <package>` for the same, with completion
over the directories here.

yay treats the directory as a git checkout and runs `git reset --hard
HEAD` in it before building, so the repository needs at least one
commit; the build leaves `src/`, `pkg/`, the upstream clone and the
package next to the PKGBUILD, all ignored.

Nothing tracks updates. To bump a `-git` package: `yay -Bi` again — the
`pkgver()` function takes the revision from the fresh clone; then copy
the version it printed into `pkgver=` in the PKGBUILD and regenerate the
metadata so the two agree:

    makepkg --printsrcinfo > .SRCINFO
