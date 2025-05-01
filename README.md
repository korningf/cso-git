# Aegis-git

Extended gitbash (Git for windows) to include MSYS2 pacman package manager.

Add unix password-store (pass command); configure with ssh, ssl, gpg, tree.

Add MSYS2 MinGW64 standard development tools (GNU autotool, glibc, gcc, etc).


# Preparation

To get pacman working we to add the gpg key for the git-sdk-64 distribution in the keyring.

It turns out it has the same author and the same key as the git-for-windows distribution!


```bash
curl -L \
  https://raw.githubusercontent.com/git-for-windows/build-extra/HEAD/git-for-windows-keyring/git-for-windows.gpg | \
  pacman-key --add - && \
  pacman-key --lsign-key E8325679DFFF09668AD8D7B67115A57376871B1C && \
  pacman-key --lsign-key 3B6D86A1BA7701CD0F23AED888138B9E1A9F3986
```


# Installation

From a gitbash shell run `install-pacman-git-bash.sh` for the initial setup.

This installs the binaries, and sets up a mirror of the MSYS2 git-sdk-64 repo.


```bash
./install-pacman-git-bash.sh
```

  

# Configuration

Update the pacman distro


First we update the pacman distribution itself.

```bash
pacman -Syy --overwrite \*
pacman -Syu --overwrite \*
```

Then we update util-linux and some core utils.

```bash
pacman -Syu util-linux --overwrite \*
pacman -Syuq tree pass  --overwrite \*
pacman -Syuq zip rsync  --overwrite \*
```


# Operation

We can now run pacman normally.



# Troubleshoot



# Attribution

Alex Sarmiento for GitPortable-Pacman and David Gleba for a later port

[gitportable-pacman](https://github.com/dgleba/gitportable-pacman)


Johannes Schindelin and GitForWindows

[git for windows](https://gitforwindows.org/install-inside-msys2-proper.html)


