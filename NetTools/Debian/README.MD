# System info

## tools
```
# Default
sipcalc ethtool traceroute whois nmap netcat wget curl nicstat telnet ping ssh dig scp rsync netstat host
nslookup

# Optional

mtr fierce lynis nikto WPScan

```

# Build Steps

## Install Debian trough powershell
* `wsl.exe --install -d Debian`

## Configure user on WSL prompt

## Install system dependencies
* ```
    sudo apt update && sudo apt install -y lldpad libcap2-bin
  ```

## Install common tools
* `sudo apt install -y sipcalc dnsutils net-tools snmp ethtool traceroute whois nmap netcat curl wget nicstat telnet`

# Optional tools

## System
* system tools
    - `sudo apt install -y git tmux vim rkhunter gcc g++ make nodejs python3 python3-pip gpgv2 dirmngr libssl1.0-dev`
    - feel free to replace tmux and vim with your choices EX: screen & nano
* [NodeJS](https://github.com/nodesource/distributions)
    - `curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -`
* [RVM](https://rvm.io/rvm/install)
    - `gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB`
    - `curl -L get.rvm.io | bash -s stable`
* [Yarn](https://yarnpkg.com/)
    - `sudo corepack enable`
    - `yarn set version stable`

## Install [MTR](https://github.com/traviscross/mtr.git)
* `git clone https://github.com/traviscross/mtr.git && cd mtr`
* Build with `./bootstrap.sh && ./configure && make`
* Add [capabilities](https://github.com/traviscross/mtr/blob/master/SECURITY#L25) `setcap cap_net_raw+ep mtr-packet`
* Test `sudo ./mtr google.com`
* Install `sudo make install`
    - Note that mtr-packet must be suid-root because it requires access to raw IP sockets. See SECURITY for security information. [Ref](https://github.com/traviscross/mtr/blob/master/SECURITY)
    - Older versions used to require a non-existent path to GTK for a correct build of a non-gtk version while GTK was installed. This is no longer necessary. `./configure --without-gtk` should now work. If it doesn't, try `make WITHOUT_X11=YES` as the make step.

## Install [Lynis](https://cisofy.com/lynis/#installation)
- Lynis is light-weight and easy to use. Although most users will install Lynis via a package, installation is not required! Just extract the archive (tarball) and run ./lynis audit system

## Install [Fierce](https://github.com/mschwager/fierce)
* Requires Python3 `python3 -m pip install fierce`

## Install [Nikto]()
* `git clone https://github.com/sullo/nikto`
* `echo 'alias nikto="perl ~/nikto/program/nikto.pl"' >> ~/.bashrc`

## Install [WPScan](https://github.com/wpscanteam/wpscan)
* Requires Ruby >= 2.5 `gem install wpscan`


# WIP

## Install [Skipfish](https://gitlab.com/kalilinux/packages/skipfish/)
* Download source
    - From google `wget -O skipfish_source.zip https://storage.googleapis.com/google-code-archive-source/v2/code.google.com/skipfish/source-archive.zip && unzip skipfish_source.zip`
    - From kali linux packages `git clone https://gitlab.com/kalilinux/packages/skipfish/`
* `cd skipfish && make`

## Install [yersinia](https://github.com/tomac/yersinia)
* ....

## Install [OpenVas OSS/free](https://github.com/greenbone/)
* ```
    sudo apt install -y bison cmake gcc-mingw-w64 heimdal-dev libgcrypt20-dev libglib2.0-dev libgnutls28-dev \
    libgpgme-dev libhiredis-dev libksba-dev libmicrohttpd-dev git libpcap-dev libpopt-dev libsnmp-dev libsqlite3-dev \
    libssh-gcrypt-dev xmltoman libxml2-dev perl-base pkg-config python3-paramiko python3-setuptools uuid-dev \
    redis-server doxygen libical-dev python-polib gnutls-bin
  ```


# References

- https://github.com/nicolaka/netshoot
- https://endjin.com/blog/2021/11/setting-up-multiple-wsl-distribution-instances
- https://github.com/Microsoft/WSL-DistroLauncher#Introduction
- https://github.com/greenbone/
- https://github.com/mschwager/fierce
- https://cisofy.com/lynis
- https://github.com/traviscross/mtr.git
- https://yarnpkg.com/
- https://github.com/nodesource/distributions
- https://github.com/tomac/yersinia
- https://code.google.com/archive/p/skipfish/
- https://wpscan.com/wordpress-security-scanner
- https://cirt.net/Nikto2