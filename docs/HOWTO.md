
# HOW TO BUILD YOUR OWN FIRMWARE
1. Make sure you have these packages preinstalled in your host:
  * gcc make patch python3 python3-pip wget diffstat chrpath rpcgen lz4 zstd cross-arm-none-eabi-gcc
2. Make sure you have at least 50Gb of available space
3. Do at least a quick read of Yocto's Project Quick build doc: http://docs.yoctoproject.org/brief-yoctoprojectqs/index.html
4. Clone this repository in your computer
5. Go to the folder where you downloaded your copy and run `./init.sh`<br>
The init script should do the following things for you
  * Get the modem's bootloader source
  * Get the ARM toolchain to build the bootloader
  * Get Yocto build source
  * Get the specific layers and dependencies to build it all
  * Initialize yocto and add the bitbake layers to the env
6. Run `make`, to see what you can build:
  - `make everything` Build Bootloader, System and Recovery and pack it
  - `make aboot` build the LK bootloader
  - `make kernel` Build the kernel and place a bootable image in target/
  - `make root_fs` Build the kernel and rootfs without proprietary blobs and place both in target/
  - `make recovery_fs` will initialize Yocto’s build environment if it wasn’t already done before, and will build a bootable image that fits into the recovery partition to make debugging easier. I've left two scripts: recoverymount and rootfs mount that mount either of the rootfs partitions into /tmp so you can make modifications to the running image more easily
  - `make clean` Will remove build and temporary directories
  - `make target_extract` Will dump the contents of the generated image to target/dump so you can examine the contents of what you're pushing (you'll need python and python's CRC and LZO modules for it to work - check out [UBIDUMP here](https://github.com/nlitsme/ubidump))
  - `make target_clean` Removes the target directory contents
  - `make aboot_clean` Cleans the LK bootloader build folder along with the generated binary
  - `make yocto_clean` Removes Yocto's temporary folder
  - `make yocto_cleancache` Removes Yocto's sstate-cache in case you need to force a rebuild while working on recipes
