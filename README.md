# Apt Miroring Help
 - Guide for apt-mirror'ing: (https://danie1.me/2019/01/14/how-to-download-ubuntu-18-04-bionic-repository-for-offline/)
 - Tool for generating sources.list: (https://repogen.simplylinux.ch/generate.php)

## Creating mirror

### Install dependencies

```sudo apt install gnupg apt-key apt-mirror wget curl```

### Setup mirror settings

Copy `mirror.list` to `/etc/apt/mirror.list`

```cp mirror.list /etc/apt/mirror.list```

Modify the line `set base_path    /path/to/files`. `/path/to/files` --> your path to where you want the mirror files stored

### Install keys before mirroring

```bash
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys C6DAEA80
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7A51D6F2
sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 614C4B38
wget -q https://dl.google.com/linux/linux_signing_key.pub -O- | sudo apt-key add -
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 93330B78
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 1378B444
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv 7F0CEB10
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys  247510BE 
wget -q http://liveusb.info/multisystem/depot/multisystem.asc -O- | sudo apt-key add -
sudo wget -O - http://deb.opera.com/archive.key | sudo apt-key add -
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys EEA14886
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 4BB9F05F
wget -O - http://www.bchemnet.com/suldr/suldr.gpg | sudo apt-key add -
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA5DFFC
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 886DDD89
wget http://www.webmin.com/jcameron-key.asc -O- | sudo apt-key add -
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 8844C542 
wget -qO - https://download.sublimetext.com/sublimehq-pub.gpg | sudo apt-key add -
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
wget -O - https://www.inetsim.org/inetsim-archive-signing-key.asc | sudo apt-key add -
sudo apt-key adv --keyserver hkp://keys.gnupg.net --recv-keys 7D8D0BF6
```

### Start mirror

```apt-mirror```

Wait a day or two.


## Host the mirror

Substitute /path/to/files with where the files are hosted:

```docker run -dit --rm --name apt -p 1804:80 -v /path/to/files:/usr/local/apache2/htdocs httpd:alpine```

## Configure new machine

```cp sources.list /etc/apt/sources.list```

Change `insertyourhostnamehere` to the IP of the mirror host.

```apt update```
