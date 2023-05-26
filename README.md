# influx-yocto-base

## HOW TO USE


## Setup host OS

==================================

    For this build we recomended for host OS to us Ubuntu 22.04

Install Ubuntu 22.04 
After install Ubuntu 22.04 run

`sudo apt-get update`

`sudo apt-get install gawk wget git-core diffstat unzip texinfo \ gcc-multilib build-essential chrpath socat \ libsdl1.2-dev xterm sed cvs subversion \ coreutils texi2html docbook-utils python-pysqlite2 help2man make \ gcc g++ desktop-file-utils libgl1-mesa-dev libglu1-mesa-dev \ mercurial autoconf automake groff curl lzop asciidoc u-boot-tools`

##### Install the repo tool

The repo tool has been developed to make it easier to manage multiple Git repositories. Instead of downloading each repository separately the repo tool can download all with one instruction. Download and install the tool by following the>

1. Create a directory for the tool. The example below creates a directory named bin in your home folder.

 `mkdir ~/bin`

2. Download the tool

 `curl http://commondatastorage.googleapis.com/git-repodownloads/repo > ~/bin/repo`

3. Make the tool executable

 `chmod a+x ~/bin/repo`

4. Add the directory to the PATH variable. The line below could be added to your .bashrc file so the path is available in each started shell/terminal

 `export PATH=~/bin:$PATH`

##### Download Yocto recipes

The Yocto project consists of many recipes used when building an image. These recipes come from several repositories and the repo tool is used to download these repositories.

In step 7 below a branch must be selected of the influx-yocto-base repository. This table lists the available branches.

|Branch name    | Description |
|-------------- | ------------| 
|influx-5.15.32 | u-boot: 2022.04. Linux: 5.15.32 |


5. Create a directory for the downloaded files (influx-bsp in the example below)

 `mkdir influx-bsp`

 `cd influx-bsp`

6. Configure Git if you haven’t already done so. Change "Your name" to your actual name and "Your e-mail" to your e-mail address.

 `git config --global user.name "Your name"`

 `git config --global user.email "Your e-mail"`

7. Initialize repo. The file containing all needed repositories is downloaded in this step. Change <selected branch> to a branch name according to the table above.

 `repo init -u https://github.com/InfluxTechnology/influx-yocto-base -b <selected branch>`

8. Start to download files

 `repo sync`

All files have now been downloaded into the influx-bsp directory. Most of the files will actually be available in the sub-directory called sources.
 
 ## Build an image
================================
 
 1. Initialize build. Before starting the build, it must be initialized. In this step the build directory and local configuration files are created. 
 
 `source influx-setup-release.sh -b build-dir`
 
  To start a build with Mender support, execute this command
 
 `source influx-setup-release.sh -b build-dir -m influx-mender.xml` 
 
 2. Starting the build. Everything has now been setup to start the actual build. Please note that depending on the capabilities of your host computer building an image can take many hours.
 
 `bitbake redge-image-base`
 
 3. Restart the build. If you need to restart a build in a new terminal window or after a restart of the host computer you don’t need to run the influx-environment-setup script again. Instead, you run the setup-environment script
 
 `source setup-environment build-dir`

 4. Deploy the image. In build folder have a script, it collect needed files for deploy.
 
 `deploy-image.sh`
