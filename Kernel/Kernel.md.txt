# 1. Host and target setup
##Source code and course materials
1)You can access all the course materials from the github link below

https://github.com/niekiran/linux-device-driver-1.git

2)Please download the course presentation slides from the link below

https://1drv.ms/b/s!Akhv68fruLVPunnvLBoIL0-Gu-et?e=cCnfvr

# 3 Host: PC with Ubuntu 18.04 OS 32/64 bit
sudo apt-get update
sudo apt-get install build-essential lzop u-boot-tools net-tools bison flex libssl-dev libncurses5-dev libncursesw5-dev unzip chrpath xz-utils minicom wget git-core
 
##workspace folder structure:
- workspace/ldd
     |
	-custom_drivers (our dev 
     |
	-downloads ( prebuilt images/SD Boot(sd boot contais pre built images)-(provided by udamy untar zip))
     |
	-patches
     |
	-source

 
# Download boot images and Root file system
1st do partision of micro sd card in to 2 parts one for BOOT and another for ROOTFS(ROOT_FILE_SYS)
2nd download root file system from site (beagleboard.org)/-> latest software images(download latest image with IOT extanction)  
