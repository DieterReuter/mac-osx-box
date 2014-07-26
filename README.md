# mac-osx-box

How-To for creating an OSX box the Vagrant way.


## Three easy step to do
1. fetch an 'Mavericks.app' from AppStore
2. prepare the OSX basebox
3. create a Vagrantfile


## Step 1: fetch an 'Mavericks.app' from AppStore

After completing this step, you'll have an `Install OS X Mavericks.app` ready on your disk drive.

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

Here we just use `box-cutter` and the [osx-vm](https://github.com/box-cutter/osx-vm).


## Step 3: create a Vagrantfile



# Licensing
Copyright (c) 2014 Dieter Reuter

MIT License, see LICENSE.txt for more details.