# influx-yocto-base


## Default branch

This default branch is based on Linux:5.15.32 and u-boot:2022.04.
It is under construction and can be used only for test purposes.

1. Create a directory for the downloaded files ('build' in the example below)

 `mkdir build`

 `cd build`

2. Initialize repo. The file containing all needed repositories is downloaded in this step.

 `repo init -u https://github.com/InfluxTechnology/influx-yocto-base -b main`

3. Start to download files

 `repo sync`

All files have now been downloaded into the 'build'. Most of the files will actually be available in the sub-directory called sources.
