# Samsung_Galaxy_Express_Prime-SM-J320a
Test root shell for any android phone with app-process32


This is nothing more than a test. It is a limited root shell, the test is to see how much can be done in the current contex.

to use the test
download or clone and (read the contents first is allways safer) run the one-click-root.bat
It will push 4 files to /data/local/tmp on your phone, it will use the "dirtycow" exploit to 
replace (temporaryly) the app_precess32 on /system/bin
then that will "fork" a shell as root.
next command will injesct the contents of the cp_comand.txt to that shell.
proof of concept you should see you can create files as and owned by root now.

The road block from here is the contex of the root. I try to cp from /dev/block to pull recovery and boot, but get permission denied
on my samsung. On my other phone it works 

I put this in the public for hope of colaberation and further the effort.
