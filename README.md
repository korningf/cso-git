# Aegis-git

![gitbash-pacman](gitbash-pacman.png)

Aegis-Git is a GitBash portable POSIX augmented with the MSYS2 pacman package manager.

It is based on GitBash, based on MSysGit, based on Msys2, itself derived from Cygwin.

GitBash ports Git and core-utils on Windows, but it does not port other needed tools.

Tools that are fundamental for build development, systems integration, and automation.

In short, Aegis-Git empowers Cloud-Ops and Dev-Ops from a bare minima Windows desktop.






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



# Extension

Add pass (POSIX password-store) and tree and configure with ssh, ssl, gpg, tree.

Add MSYS2 MinGW64 standard development toolchain (GNU autotool, glibc, gcc, etc).



# Attribution


*Stephane Korning* (stefuss@yahoo.com) for the idea adn impetus to port pacman to gitbash. 


*Alex Sarmiento* and *David Gleba* for an actual implementation in their GitPortable-Pacman.

[gitportable-pacman](https://github.com/dgleba/gitportable-pacman)


*Johannes Schindelin* for Git-For-Windows and its underlying git-sdk-64 (Herculean work!).

[git for windows](https://gitforwindows.org/install-inside-msys2-proper.html)


The host of developers having made *Git*, *Msys*, *Cygwin*, *MinGW*, *GNU* and *POSIX* possible.



# License

Creative-Commons,  Attribution, NonCommercial, ShareAlike 4.0


