# mac-osx-box

How-To for creating an OSX box the Vagrant way.


## Three easy step to do
1. fetch an 'Mavericks.app' from AppStore
2. prepare the OSX basebox
3. create a Vagrantfile


## Prerequisites
1. we need [Packer](http://www.packer.io)
2. we need [Vagrant](http://www.vagrantup.com)
3. we need [VirtualBox](https://www.virtualbox.org) --or--
3. we need [VMware Fusion](http://www.vmware.com/products/fusion/)


## Step 1: fetch an 'Mavericks.app' from AppStore

After completing this step, you'll have an `Install OS X Mavericks.app` ready on your disk drive.


Here are some instructions how you can download an App from the AppStore and easily access the Installer(.dmg), see http://derflounder.wordpress.com/2013/08/22/downloading-apples-server-app-installer-package/

First step is to enable the "Debug" menu in the "App Store" App.
```bash
defaults write com.apple.appstore ShowDebugMenu -bool true
```

For your convenience we just store that in our `iso structure` in `~/iso/osx/Mavericks/`
```bash
ls -al ~/iso/osx/Mavericks/
total 16
drwxr-xr-x  3 dieterreuter  staff   136 Jul 26 13:28 .
drwxr-xr-x  3 dieterreuter  staff   136 Jul 26 13:26 ..
-rw-r--r--@ 1 dieterreuter  staff  6148 Jul 26 13:28 .DS_Store
drwxr-xr-x  3 dieterreuter  staff   102 Nov  2  2013 Install OS X Mavericks.app
``` 


## Step 2: prepare the OSX basebox with `box-cutter`

We just use `box-cutter` to create a basebox and here the [box-cutter/osx-vm](https://github.com/box-cutter/osx-vm).
```bash
git clone https://github.com/box-cutter/osx-vm.git
cd osx-vm
```

For more details to prepare the ISO follow the [box-cutter docs](https://github.com/box-cutter/osx-vm/blob/master/README-timsutton.md).
```bash
sudo prepare_iso/prepare_iso.sh ~/iso/osx/Mavericks/Install\ OS\ X\ Mavericks.app/ out
```
...this gives us some output like
```bash
-- Destination dir out doesn't exist, creating..
-- Attaching input OS X installer image with shadow file..
-- Mounting BaseSystem..
-- OS X version detected: 10.9., build 13A603
-- Making firstboot installer pkg..
-- Converting BaseSystem.dmg to a read-write DMG located at /tmp/veewee-osx-basesystem-rw.DKHz.dmg..
-- Growing new BaseSystem..
-- Mounting new BaseSystem..
-- Moving 'Packages' directory from the ESD to BaseSystem..
-- Adding automated components..
-- Unmounting BaseSystem..
-- Unmounting ESD..
-- On Mavericks the entire modified BaseSystem is our output dmg.
-- Fixing permissions..
-- Checksumming output image..
-- MD5: 22d1358cfc2d885200468912191283a2
-- Done. Built image is located at out/OSX_InstallESD_10.9_13A603.dmg. Add this iso and its checksum to your template.
```
```bash
ls -al out/
total 10378528
drwxr-xr-x   2 dieterreuter  staff         102 Jul 26 14:59 .
drwxr-xr-x  10 dieterreuter  staff         646 Jul 26 14:57 ..
-rw-r--r--@  1 dieterreuter  staff  5313805837 Jul 26 15:02 OSX_InstallESD_10.9_13A603.dmg
```

Now, let's build the basebox using `Packer`.
```bash
mkdir -p "iso/OS X Mavericks"
touch "iso/OS X Mavericks/Install OS X Mavericks.app"
mkdir -p dmg
cp ./out/OSX_InstallESD_10.9_13A603.dmg dmg/OSX_InstallESD_10.9_13A603.dmg
touch dmg/OSX_InstallESD_10.9_13A603.dmg
make vmware/osx109
```


## Step 3: create a Vagrantfile


We need to install the Vagrant plug-in `vagrant-serverspec`
```bash
vagrant plugin install vagrant-serverspec
```



# Licensing
Copyright (c) 2014 Dieter Reuter

MIT License, see LICENSE.txt for more details.