# Aegis-git

Extended gitbash (Git for windows) to include MSYS2 pacman package manager.

Add unix password-store (pass command); configure with ssh, ssl, gpg, tree.

Add MSYS2 MinGW64 standard development tools (GNU autotool, glibc, gcc, etc).


# Installation

From a gitbash shell run `sh install-pacman-git-bash.sh` for the initial setup.

This installs the binaries, and sets up a mirror of the MSYS2 git-sdk-64 repo.

This will fail as we are missing the distro key for git-sdk-64 in the keyring.

It turns out this is the same key as the git-for-windows distro.


# Configuration

Add the git-for-windows key the keyring.

```bash
curl -L \
  https://raw.githubusercontent.com/git-for-windows/build-extra/HEAD/git-for-windows-keyring/git-for-windows.gpg | \
  pacman-key --add - && \
  pacman-key --lsign-key E8325679DFFF09668AD8D7B67115A57376871B1C && \
  pacman-key --lsign-key 3B6D86A1BA7701CD0F23AED888138B9E1A9F3986
```

# Operation



Update the pacman distro


```bash
pacman -Sy
pacman -Syu --overwrite ‘*’
```



You can now run pacman normally.

```bash
pacman -Syuq tree pass
pacman -Syuq zip rsync
```


# Troubleshoot

  https://bbs.archlinux.org/viewtopic.php?id=272350
  https://ostechnix.com/how-to-solve-error-failed-to-commit-transaction-conflicting-files-in-arch-linux/

# Attribution

Alex Sarmiento for GitPortable-Pacman and David Gleba for a later port

[gitportable-pacman](https://github.com/dgleba/gitportable-pacman)


Johannes Schindelin and GitForWindows

[git for windows](https://gitforwindows.org/install-inside-msys2-proper.html)


