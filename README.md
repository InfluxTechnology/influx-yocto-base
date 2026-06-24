# influx-yocto-base

Yocto BSP setup for InfluxTechnology devices.  
- **Linux version:** 6.6.23  
- **U-Boot version:** 2024.04  

## Required Packages

The Yocto Project requires several packages to be installed on the host machine.
```bash
sudo apt-get install gawk wget git-core diffstat unzip texinfo
gcc-multilib build-essential chrpath socat libsdl1.2-dev xterm sed cvs subversion
coreutils texi2html docbook-utils python-pysqlite2 help2man make
gcc g++ desktop-file-utils libgl1-mesa-dev libglu1-mesa-dev
mercurial autoconf automake groff curl lzop asciidoc u-boot-tools
```

---


## Setup repo tool

Install repo
```bash
mkdir -p ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
export PATH=~/bin:$PATH
```

Configure Git
```bash
git config --global user.email "you@example.com"
git config --global user.name "Your Name"
```

---

## Configure repo to use private repository

Create `~/.netrc` file with content:
```text
machine github.com
login superflay123@gmail.com
password private_key_here ghp_*************************
```

---

## Default branch 

Create a directory for the downloaded files (`build` in the example below):
```bash
mkdir build
cd build
```

Initialize repo. The file containing all needed repositories is downloaded in this step 
```bash
repo init -u https://github.com/InfluxTechnology/linux-rexgen-base -b influx-6.6.23 -m base.xml 
```
Start to download files:
```bash
repo sync
```

All files have now been downloaded into the `build` directory.  
Most of the files will actually be available in the sub-directory called `sources`.

---

##  Build an image

Initialize build. Before starting the build, it must be initialized. In this step, the build directory and local configuration files are created.
```bash
source influx-setup-release.sh -b build-dir
```

Starting the build. Everything has now been set up to start the actual build. Please note that building an image can take many hours, depending on your host computer's capabilities.
```bash
bitbake influx-image-басе
```

Don't restart the build. If you need to restart a build in a new terminal window or after a restart of the host computer, you don’t need to rerun the influx-setup script. Instead, you run the setup-environment script.
```bash
source setup-environment build-dir
```
