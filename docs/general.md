[Back to index](./index.md)

# General commands

## changing system hostname

```bash
echo "192.168.18.50 myhost.example.com" | sudo tee -a /etc/hosts
sudo hostnamectl set-hostname myhost.example.com
```

Replace myhost.example.com with your correct hostname/valid domain name.
In a local environment behind a fritz.box router, this would be `myhost.fritz.box`.

## install cockpit

Let's install it on Raspberry Pi. Official installation document of the Cockpit says run the command below for Debian 9. If you'll run some other distro, run `cat /etc/*-release` to determine your linux distro, and find the installation option fits for you.

```bash
echo 'deb http://deb.debian.org/debian stretch-backports main' > /etc/apt/sources.list.d/backports.list
apt-get update
sudo apt-get install cockpit
```

If you're having problems about permissions, simply to `sudo su` and run the commands, and `exit` from sudo

Probably you'll have another issue with key signing, like:

```
$ apt-get update
...
Fetched 13.2 MB in 28s (456 /kBs)
Reading package lists... Done
W: GPG error: http://deb.debian.org/debian stretch-backports InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 8B48AD6246925553 NO_PUBKEY 7638D0442B90D010
W: The repository 'http://deb.debian.org/debian stretch-backports InRelease' is not signed.
N: Data from such a repository can't be authenticated and is therefore potentially dangerous to use.
N: See apt-secure(8) manpage for repository creation and user configuration details.
```

We'll download keys from ubuntu key server. You need to first install dirmngr to download valid keys from a server.

```bash
apt-get install dirmngr --install-recommends
```

Now, you can run `apt-key adv` commands for each key,

```bash
run apt-key adv --keyserver keyserver.ubuntu.com --recv 7638D0442B90D010
run apt-key adv --keyserver keyserver.ubuntu.com --recv 8B48AD6246925553
```

Let's do:

```bash
$ apt-key adv --keyserver keyserver.ubuntu.com --recv 7638D0442B90D010
Executing: /tmp/apt-key-gpghome.vJbRXc9SQt/gpg.1.sh --keyserver keyserver.ubuntu.com --recv 7638D0442B90D010
gpg: key 7638D0442B90D010: 13 signatures not checked due to missing keys
gpg: key 7638D0442B90D010: public key "Debian Archive Automatic Signing Key (8/jessie) <ftpmaster@debian.org>" imported
gpg: Total number processed: 1
gpg:               imported: 1
$ apt-key adv --keyserver keyserver.ubuntu.com --recv 8B48AD6246925553
Executing: /tmp/apt-key-gpghome.4KvMYBUegX/gpg.1.sh --keyserver keyserver.ubuntu.com --recv 8B48AD6246925553
gpg: key 8B48AD6246925553: 28 signatures not checked due to missing keys
gpg: key 8B48AD6246925553: public key "Debian Archive Automatic Signing Key (7.0/wheezy) <ftpmaster@debian.org>" imported
gpg: Total number processed: 1
gpg:               imported: 1
```

We're ready to go, lets run the update again;

```bash
$ apt-get update
Get:1 http://archive.raspberrypi.org/debian stretch InRelease [25.4 kB]
Hit:2 http://raspbian.raspberrypi.org/raspbian stretch InRelease
Get:3 http://deb.debian.org/debian stretch-backports InRelease [91.9 kB]
Fetched 117 kB in 3s (34.3 kB/s)
Reading package lists... Done
```

And let's install the Cockpit

```bash
apt-get install cockpit
```

When it's done, go to `https://LINUX_DEVICE_IP:9090/` on your browser to access your Cockpit. You can login with the linux user on web UI. That's it. We're in.
