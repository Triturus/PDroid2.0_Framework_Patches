<p align="center">
  <img src="http://www.privilege-car.de/xda/PDroid-banner.png" alt="PDroid2.0"/>
</p>
## PDroid2.0 Official Framework Patches
These are the patches for the official PDroid2.0 framework. The patches only contain the latest stable version. I'm currently looking for a way to distribute 'devel' patches which are for testing purpose only. If someone has good ideas, please get in touch with me.

### Applying the patches
**1. For first-timers**

Make sure your environment is setup, i.e. you ran

	cd <top-of-your-source-tree>
	. build/envsetup.sh

from the top of your Android source tree.

Get the repository containing the framework patches. Put them outside of your source tree and run ppatch

	cd <somewhere-but-not-in-your-source-tree>
	git clone git://github.com/CollegeDev/PDroid2.0_Framework_Patches.git ppatches
	ppatches/ppatch install

That's it.

**2. For second-timers, third-timers, ...** 

	cd <top-of-your-source-tree>
	. build/envsetup.sh
	cd <where-you-put-the-patches--i-hope-it-is-not-in-your-source-tree>
	git pull
	./ppatch update

That's it.

**3. For last-timers**

	cd <top-of-your-source-tree>
	. build/envsetup.sh
	cd <are-your-sure-they-are-not-in-your-source-tree--well-now-it-does-not-matter-anymore>
	./ppatch remove

That's it.


### Apply The Patches manually
I'm also looking forward for an better way how to apply the patches. The **yourEnvDir** is the main source directory (e.g. it contains the framework-,build-, and libcore directory):

**1. Step**	

    cd ~/yourEnvDir; repo sync -j16 -f 
    //if sync hangs at 100% try following, otherwise skip this!
    // begin commands for hanging sync!
    press strg+z
    kill %1
    repo sync -j16 -l
    // end commands for hanging sync!
	git checkout -b pdroid; patch -p1 < ~/CM10.1_build.patch
	git checkout -b pdroid; patch -p1 < ~/CM10.1_libcore.patch
	git checkout -b pdroid; patch -p1 < ~/CM10.1_Mms.patch
	git checkout -b pdroid; patch -p1 < ~/CM10.1_framework.patch
	git checkout -b pdroid; patch -p1 < ~/CM10.1_PDAgent.patch
	
**2. Step**

Now you have to decide which **default-deny-mode** you prefer. If you don't know what it is, please read [this](http://forum.xda-developers.com/showpost.php?p=37742535&postcount=623) post at topic **hardcoded default deny mode**. You can simply change the default deny mode, by open the class **PrivacySettings.java** from package android.privacy [directory: frameworks/base/privacy/java/android/privacy/PrivacySettings.java] with a texteditor. Then change following line:

    public static final int CURRENT_DEFAULT_DENY_MODE = DEFAULT_DENY_EMPTY;

To the demanded cases:

**REAL**

    public static final int CURRENT_DEFAULT_DENY_MODE = DEFAULT_DENY_REAL;
    
**RANDOM**

    public static final int CURRENT_DEFAULT_DENY_MODE = DEFAULT_DENY_RANDOM;
    
**EMPTY**

    public static final int CURRENT_DEFAULT_DENY_MODE = DEFAULT_DENY_EMPTY;

**3. Step**

Now you can just build your sources by using following commands:
   
    . build/envsetup.sh 
    brunch <YOUR_DEVICE>
    
**IMPORTANT**
If you have previous patches applied (e.g. v1.54) you have to delete the folder

    packages/apps/Settings
    
**before** you sync your repo!

### Remove The Patches
You can remove the Patches with following commands:

	cd yourEnvDir/build ; git checkout . ; git clean -df
	cd yourEnvDir/libcore ; git checkout . ; git clean -df
	cd yourEnvDir/frameworks/base ; git checkout . ; git clean -df
	cd yourEnvDir/frameworks/opt/telephony ; git checkout . ; git clean -df
	cd yourEnvDir/packages/apps/Mms ; git checkout . ; git clean -df
	rm -rf yourEnvDir/packages/apps/PDroidAgent
	cd yourEnvDir
	repo abandon pdroid
    
Now only clean your target directory:

	make clobber && make clean

### Easier Way?
If you aren't able to compile by your own, please choose the [PDroid2.0-Flash-Repo](http://forum.xda-developers.com/showpost.php?p=32458186&postcount=2) download ready builds for your ROM and Device.

### Can I help you?
Yes of course, I'm always in search of **Team-Members** and **contributors** for other ROMs. If you want to help me, just get in touch with me :-)
