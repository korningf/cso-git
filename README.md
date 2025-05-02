# Aegis-git

![gitbash-pacman](gitbash-pacman.png)

Aegis-Git is a GitBash portable POSIX augmented with the MSYS2 PacMan package manager.

It is based on GitBash, based on MSysGit, based on Msys2, itself derived from Cygwin.

GitBash ports Git and core-utils on Windows, but it does not port other needed tools.

Tools that are fundamental for build development, systems integration, and automation.

Aegis-Git empowers Cloud-Ops and Dev-Ops automation from a bare minimum Windows desktop.


# Mission

Different institutions or individuals vary widely in their desktop security practices.

Some may allow a full Cygwin POSIX dstribution, others MSsys, yet others merely GitBash.

We want a minimum POSIX environment for automation and integration on Windows Desktops.


.

For Automation we need to authenticate, pull code from a repo, and run secure commands.

We start with GitBash as baremetal base box, an atomic building block for other systems.

It should have, at minimum

- POSIX bash shell
- SSH Secure Shell
- GNU core utils
- package manager
- Git SCM



# Solution

GitBash covers almost everything we need. The only thing missing is a package manager.

The key to getting this to work is to realise that underneath GitBash is a minimal MSys.

It is an MSys2 pared-down without a MinGW toolchain and without any package management.

But GitBash itself is built on MSys2, specifically, inside SysGit / MSysGit, which does.

We can clone its pacman package management configuration and repatriate it into gitbash.



# Preparation

*You should uninstall any other competing variants of GitBash, MSysGit, or GitForWindows*.

We want Aegis-git to be multi-user and crucially be able to run system daemons and servers.

These typically run as technical service accounts and should not live in a user `%AppData%`. 

.

For this reason, though we may have user-space install, we still want it to live in `c:\git`.

We recommend doing an initial gitbash install as Administrator along with the `sshd` Daemon.

User-space installs will not be able to run the `sshd` OpenSSH server or any other daemon.

Other than that, User-space install works just fine - we still recommend it lives in `c:\git`. 

.

install gitbash:

    winget install --id Git.Git -e --source winget --location "c:\git"



# Installation


To get pacman working we to add the gpg key for the git-sdk-64 distribution in the keyring.

It turns out it has the same author and the same key as the git-for-windows distribution!


install keyring:

```bash
curl -L \
  https://raw.githubusercontent.com/git-for-windows/build-extra/HEAD/git-for-windows-keyring/git-for-windows.gpg | \
  pacman-key --add - && \
  pacman-key --lsign-key E8325679DFFF09668AD8D7B67115A57376871B1C && \
  pacman-key --lsign-key 3B6D86A1BA7701CD0F23AED888138B9E1A9F3986
```


install pacman:

From the gitbash shell run `install-pacman-git-bash.sh` for the initial setup.

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


