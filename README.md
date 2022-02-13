# AUR

Privateness in the Arch User Repos


## Package Maintenance

This repository allows PKGBUILDs to be maintained in the [AUR](https://aur.archlinux.org) for corresponding [NESS-network](https://github.com/NESS-network) github repos.

The old method of managing AUR packages
```
git clone ssh://aur@aur.archlinux.org/$PACKAGE.git
updpkgsums
makepkg --printsrcinfo > .SRCINFO;
git add -f PKGBUILD .SRCINFO
git commit -m "commit message"
git push
```

with `aurpublish` and a containing github repository this becomes:

```
# initial setup step, pull package from AUR
aurpublish -p $PACKAGE
#change some files
updpkgsums
makepkg --printsrcinfo > .SRCINFO;
git add -f PKGBUILD .SRCINFO
#add scripts, etc.
git commit -m "commit message"
#push to AUR
aurpublish $PACKAGE
#push to github
git push

```

Needed dependencies for maintainers: pacman-contrib (updpkgsums) & aurpublish

Dependencies for deb.PKGBUILDs: `dpkg`

## Testing builds

Packages are buildable with `makepkg` on arch linux, the task of handling build dependencies is fulfilled by the system package manager; `pacman`

From within any subdirectory containing a PKGBUILD (i.e. the desired repository or package to create)
```
git clone https://aur.archlinux.org/privateness
cd privateness
makepkg -sf
```

## Installing from AUR

The build and installation process is fully automated with the help of `yay`.
```
[user@linux ~]$ yay -S privateness
```
