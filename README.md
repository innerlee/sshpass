# SSHPass

SSHpass offers you the ability to automatically offer a password via SSH when
you are prompted for it.

**NEW:**
This fork supports google *two-step authentication* and *auto confirmation* with `yes`.

**NOTE:**
Check [here](https://github.com/innerlee/setup) for one-line setup script for non-`sudo`ers.

## Usage

```bash
export SSHVCODE=YOUR_GOOGLE_AUTHE_SECRET
export SSHPASS=YOUR_SSH_PASSWORD
sshpass -e -y ssh user@host
```

For jump server, edit the `~/.ssh/config` file 

```sshconfig
LogLevel ERROR

Host *
    User lizz
    ForwardAgent yes
    ServerAliveInterval 60
    ServerAliveCountMax 10

Host jumper
    HostName jumper.jumper.com

Host server
    HostName 1.2.3.4
    ProxyCommand sshpass -e -y ssh -q -W %h:%p jumper
```

## Install

```bash
# dependencies
sudo apt install oathtool
sudo apt-get install autoconf

git clone git@github.com:innerlee/sshpass.git
cd sshpass
autoreconf -f -i
./configure --prefix=$HOME/app
make -j && make install
```

### Related Projects

* https://github.com/Kxuan/sshpass OTP support
* https://github.com/jctanner/sshpass Break on pem file passphrase prompt
* https://github.com/liranms/sshpass Support for 'ssh>' prompt
