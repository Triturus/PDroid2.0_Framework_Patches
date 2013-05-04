<p align="center">
  <img src="http://www.privilege-car.de/xda/PDroid-banner.png" alt="PDroid2.0"/>
</p>
## PDroid2.0 Official Framework Patches
These are the patches for the official PDroid2.0 framework. The patches only contain the latest stable version. I'm currently looking for a way to distribute 'devel' patches which are for testing purpose only. If someone has good ideas, please get in touch with me.

### Apply The Patches
I'm also looking forward for an better way how to apply the patches. Until now I handle it the same way like mateor, so you can use this commands. The **yourEnvDir** is the main source directory (e.g. it contains the framework-,build-, and libcore directory):
	
    cd ~/yourEnvDir; repo sync -j16 -f 
    //if sync hangs at 100% try following, otherwise skip this!
    // begin commands for hanging sync!
    press strg+z
    kill %1
    repo sync -j16 -l
    // end commands for hanging sync!
	git checkout -b pdroid; patch -p1 < ~/JB_build.patch
	git checkout -b pdroid; patch -p1 < ~/JB_libcore.patch
	git checkout -b pdroid; patch -p1 < ~/JB_Mms.patch
	git checkout -b pdroid; patch -p1 < ~/JB_frameworks_base.patch
	git checkout -b pdroid; patch -p1 < ~/JB_frameworks_opt.patch
	. build/envsetup.sh 
    brunch <YOUR_DEVICE>

### Remove The Patches
You can remove the Patches with following commands (also same way like mateo handles it):

	cd ~/yourEnvDir; git checkout . ; git clean -df
	repo abandon pdroid
    
Now only clean your target directory:

	make clobber && make clean
### Easier Way?
If you aren't able to compile by your own, please choose [AutoPatcher](http://forum.xda-developers.com/showthread.php?t=1719408) to apply the patch to your current ROM.

### Can I help you?
Yes of course, I'm always in search of **Team-Members** and **contributors** for other ROMs. If you want to help me, just get in touch with me :-)
