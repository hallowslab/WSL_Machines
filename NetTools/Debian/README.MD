# System info

## tools
```
# Default
sipcalc ethtool traceroute whois nmap netcat wget curl nicstat telnet ping dig netstat host
nslookup

# Optional

mtr fierce lynis nikto WPScan

```

# Build Steps

## Install Debian trough powershell
* `wsl.exe --install -d Debian`

## Configure user on WSL prompt
* This has to be done manually for now... check [References - 3.](#references) to set up costum distros

## Install system dependencies
* `sudo apt update && sudo apt install -y lldpad libcap2-bin`

## Install common tools
* `sudo apt install -y sipcalc dnsutils net-tools snmp ethtool traceroute whois nmap netcat curl wget nicstat telnet`

## Configure user
* Configure the user in /etc/wsl.conf
    - ```
      tee -a /etc/wsl.conf <<EOF
      [user]
      default=nettools
      EOF
      ```

## Export Machine
* `wsl.exe --export Debian nettools_<version>.tar`
    - version can be minimal or full depending on included tools

## Import instance
* Create new instances `wsl --import <new distribution name> <install location> <export file name>`
    - `wsl --import NetTools .\NetTools nettools.tar`

# Optional tools

## System
* [NodeJS LTS](https://github.com/nodesource/distributions)
    - `curl -fsSL https://deb.nodesource.com/setup_16.x | sudo -E bash -`

* system tools
    - ```
      sudo apt install -y git tmux vim rkhunter gcc g++ make nodejs gpgv2 dirmngr automake autoconf pkgconf build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libsqlite3-dev libreadline-dev libffi-dev libbz2-dev
      ```
    - feel free to replace tmux and vim with your choices EX: screen & nano

* [Python 3.8.13](https://docs.python.org/3.8/)
    - `wget https://www.python.org/ftp/python/3.8.13/Python-3.8.13.tar.xz`
    - `tar -xf Python-3.8.13.tar.xz && rm -rf Python-3.8.13.tar.xz && cd Python-3.8.13`
    - `./configure --enable-optimizations && make &&  && CD ~ && cd ~`
    - `python3 -m pip install virtualenv`
    - `echo 'export PATH="$PATH:$HOME/.local/bin"' >> ~/.bashrc`

* [RVM](https://rvm.io/rvm/install)
    - `gpg --keyserver hkp://pgp.mit.edu --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB`
    - `curl -L get.rvm.io | bash -s stable`
    - `rvm install 2.6`
    - `rvm alias create default ruby-2.6`
    - refresh environment...

* [Yarn](https://yarnpkg.com/)
    - `sudo corepack enable`
    - `yarn set version stable`

## Install [MTR](https://github.com/traviscross/mtr.git)
* `git clone https://github.com/traviscross/mtr.git && cd mtr`
* Build with `./bootstrap.sh && ./configure --without-gtk --without-jansson && make`
* Add [capabilities](https://github.com/traviscross/mtr/blob/master/SECURITY#L25) `sudo setcap cap_net_raw+ep mtr-packet`
* Test `sudo ./mtr google.com`
* Install `sudo make install && cd ~`
    - Note that mtr-packet must be suid-root because it requires access to raw IP sockets. See SECURITY for security information. [Ref](https://github.com/traviscross/mtr/blob/master/SECURITY)
    - Older versions used to require a non-existent path to GTK for a correct build of a non-gtk version while GTK was installed. This is no longer necessary. `./configure --without-gtk` should now work. If it doesn't, try `make WITHOUT_X11=YES` as the make step.

## Install [Lynis](https://cisofy.com/lynis/#installation)
- Lynis is light-weight and easy to use. Although most users will install Lynis via a package, installation is not required! Just extract the archive (tarball) and run ./lynis audit system
- `git clone https://github.com/CISOfy/lynis.git`


## Install [Nikto]()
* `git clone https://github.com/sullo/nikto`
* `echo 'alias nikto="perl ~/nikto/program/nikto.pl"' >> ~/.bashrc`

## Install [WPScan](https://github.com/wpscanteam/wpscan)
* Requires Ruby >= 2.5
* `gem install wpscan`

## Install [Spiderfoot](https://www.spiderfoot.net/documentation/)
* `git clone https://github.com/smicallef/spiderfoot.git && cd spiderfoot`
* `python3 -m virtualenv venv`
* `./venv/bin/python -m pip install -r requirements.txt && cd ~`
* `echo 'alias spiderfoot="cd ~/spiderfoot && ./venv/bin/python sf.py -l 127.0.0.1:5001"' >> ~/.bashrc`

## Install [Skiptracer]https://gitlab.com/illwill/skiptracer)
* `git clone https://github.com/xillwillx/skiptracer.git skiptracer && cd skiptracer`
* 

# WIP

## Install [Fierce](https://github.com/mschwager/fierce)
Requires **Python3.6>=**
* `git clone https://github.com/mschwager/fierce.git && cd fierce`
* `python3 -m virtualenv venv`
* `./venv/bin/python -m pip install -r requirements.txt`
* `echo 'alias fierce="source venv/bin/activate && fierce"' >> ~/.bashrc`

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

1. https://github.com/nicolaka/netshoot
2. https://endjin.com/blog/2021/11/setting-up-multiple-wsl-distribution-instances
3. https://github.com/Microsoft/WSL-DistroLauncher#Introduction
4. https://github.com/greenbone/
5. https://github.com/mschwager/fierce
6. https://cisofy.com/lynis
7. https://github.com/traviscross/mtr.git
8. https://yarnpkg.com/
9. https://github.com/nodesource/distributions
10. https://github.com/tomac/yersinia
11. https://code.google.com/archive/p/skipfish/
12. https://wpscan.com/wordpress-security-scanner
13. https://cirt.net/Nikto2