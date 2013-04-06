<p align="center">
  <img src="http://www.privilege-car.de/xda/PDroid-banner.png" alt="PDroid2.0"/>
</p>
## PDroid2.0 Official Framework Patches
These are the patches for the official PDroid2.0 framework. The patches only contain the latest stable version. I'm currently looking for a way to distribute 'devel' patches which are for testing purpose only. If someone has good ideas, please get in touch with me.

### Apply The Patches
I'm also looking forward for an better way how to apply the patches. Until now you can handle it the same way like mateor, so you can use this commands:
	
    cd ~/android/system; repo sync -j16 -f
	cd ~/android/system/build; git checkout -b pdroid; patch -p1 < JB_build.patch
	cd ~/android/system/libcore; git checkout -b pdroid; patch -p1 < JB_libcore.patch
	cd ~/android/system/packages/apps/Mms; git checkout -b pdroid; patch -p1 < JB_Mms.patch
	cd ~/android/system/frameworks/base; git checkout -b pdroid; patch -p1 < JB_frameworks_base.patch
	cd ~/android/system/frameworks/opt/telephony; git checkout -b pdroid; patch -p1 < ~/JB_frameworks_opt.patch
    cd ~/android/system/frameworks/opt/telephony; git checkout -b pdroid; patch -p1 < ~/JB_Manager.patch
	cd ~/android/system; . build/envsetup.sh 
    brunch <YOUR_DEVICE>
    
Please note that the Patch **JB_frameworks_opt.patch** does not exists for CM10. Now you need to add the privacy Image to your sources. Go to directory: *yourdir/device/your_manufacturer(e.g.samsung)/your_device_model/your_device.mk* and add following to the mk file:
    # Secure Fake Image
    PRODUCT_COPY_FILES += \
    privacy/PDroid.jpeg:system/media/PDroid.jpeg

At least just copy the PDroid.jpeg to following folder (if it does not exists, create it with all subfolders):

    yourenvdir/privacy/PDroid.jpeg


### Remove The Patches
You can remove the Patches with following commands (also same way like mateo handles it):

	cd ~/android/system/build; git checkout . ; git clean -df
	cd ~/android/system/libcore; git checkout . ; git clean -df
	cd ~/android/system/frameworks/base; git checkout . ; git clean -df
	cd ~/android/system/frameworks/opt/telephony; git checkout . ; git clean -df
	cd ~/android/system/packages/apps/Mms; git checkout . ; git clean -df
	cd ~/android/system; repo abandon pdroid
    
Now only clean your target directory:

	cd ~/android/system; make clobber ; make clean
    
At least you have to delete following folders:

    packages/Apps/PDroidAgent/*
    yourenvdir/privacy/*

### Can I help you?
Yes of course, I'm always in search of **Team-Members** and **contributors** for other ROMs. If you want to help me, just get in touch with me :-)
