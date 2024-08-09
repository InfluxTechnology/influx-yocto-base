# influx-yocto-base


## Default branch

This branch is based on Linux:6.1.36 and u-boot:2023.04. Yocto mickledore relsease

It is under construction and can be used only for test purposes.

1. Create a directory for the downloaded files ('build' in the example below)

 `mkdir build`

 `cd build`

2. Initialize repo. The file containing all needed repositories is downloaded in this step.

 `repo init -u https://github.com/InfluxTechnology/influx-yocto-base -b influx-6.1.36`

3. Start to download files

 `repo sync`

All files have now been downloaded into the 'build'. Most of the files will actually be available in the sub-directory called sources.

## Build an image

1. Initialize build. Before starting the build, it must be initialized. In this step, the build directory and local configuration files are created.

'source influx-setup-release.sh -b build-dir'

2. Starting the build. Everything has now been set up to start the actual build. Please note that building an image can take many hours, depending on your host computer's capabilities.

'bitbake redge-image-base'

3. Don't restart the build. If you need to restart a build in a new terminal window or after a restart of the host computer, you don’t need to rerun the influx-environment-setup script. Instead, you run the setup-environment script.

'source setup-environment build-dir'

 4. Deploy the image. In the build folder, a script collects needed files for deployment.

'deploy-image.sh'
