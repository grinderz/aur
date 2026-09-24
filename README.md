# aur

Own PKGBUILDs — packages the AUR has in the wrong flavour or not at all.
One directory per package, with the `.SRCINFO` makepkg generates.

Build and install one with yay, which pulls the dependencies from the
repositories and the AUR:

    yay -B ~/src/personal/aur/<package>

Nothing tracks updates: bump the package and run it again.
