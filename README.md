saveItAll
=========
saveItAll is a tool that speeds up flash drive installations of Linux Mint (and other Debian Linux based distros) while maintaining data safety.

Requirements
-------------
saveItAll requires:
  * Linux Mint (or other Debian Linux-based distribution), installed on a SD card or USB drive
  * Cinnamon desktop (for now, not necessary for operation)
  * Reliable power supply
    * This is VERY important - data is not saved instantly, and a power loss could result in loss of data.
    * For laptops, ensure that you have at least 2+ hours of battery life.
    * For desktops, ensure that you have a UPS powering your PC.
  * 512 MB+ free memory to store latent file data; 1.5 GB+ recommended

Installation
-------------
1. Add the following lines to /etc/sysctl.conf:
```
vm.swappiness = 0
vm.dirty_background_ratio = 20
vm.dirty_expire_centisecs = 0
vm.dirty_ratio = 80
vm.dirty_writeback_centisecs = 0
```
2. Modify your /etc/fstab to add `noatime,data=writeback` to the mount options for
   your root filesystem.
3. If you use Firefox, disable storing of any history. Firefox tends to save frequenty,
   causing significant performance problems.
4. Install the tools into ~/saveItAll.
5. Add a launcher. Call it saveItAll, and set it to run `~/saveItAll/saveItAll`.
6. Open your menu Preferences > Startup Applications. Add another startup
   application, call it saveItAll, and set it to run `~/saveItAll/saveItAllD`.
7. Reboot the system. If it works, you should now see a new window when you
   login, and your system should be much faster!

About
------
saveItAll works by disabling the automatic save mechanism provided by the kernel, and replaces it
with a tool and background process to manually save data when you are not using your PC. When the
kernel does a save, the computer tends to stop responding, resulting in the well known
slowness of using a USB flash drive or SD card for Linux. However, when the automatic
save mechanism is disabled, the writes are buffered into memory, and only written out
when a request to write data is made. This results in a much faster, responsive system. 
saveItAll makes those requests every so often, as well as offers a tool to make a
request anytime, such as when an important document is saved.

Note that when saveItAll performs a save, the system will still become unresponsive. Just wait and
allow the save to occur, and saveItAll will notify you when the save is complete. Once the save
is complete, the system will become responsive again.

<b>It is important to note that this tool, although with good intentions, can cause harm if
not properly used.</b> Since the changes to your disk are buffered into memory, loss of power
or a hard system crash will cause the data to be lost, since they were never written to disk.
Note that this applies for ALL data transfers involved, including transfers and I/O on your
internal HDD.

**Nevertheless, this is easy to mitigate as long as the following guidelines are followed:**

  * On laptops, keey your laptop plugged in and charged at all times.
  * When your laptop is about to run out of battery, **SHUT DOWN YOUR COMPUTER**.
    When shutting down, the kernel ensures that all the data is completely saved before shutting down.
    Technically, you could do a manual save and then put it to sleep, but it does not guarantee complete
    writes, such as when applications are closed and data is written. In conclusion, when battery is low,
    SHUT DOWN!
  * On desktops, when the UPS is running on backup power, SHUT DOWN IMMEDIATELY. Do NOT take any chances.
  * When the daemon asks to save data, try your best not to cancel the save. If you cancel the save, make sure
    to run a manual save at your earliest convenience.
	
Finally, if you run certain programs, such as Firefox or LibreOffice, you may experience
some performance problems. This is due to those programs running saves manually on their
own accord. If you encounter problems, try disabling the auto-save functions or caching
functions to speed things up.

Future
-------
In the near future, a general setup tool will be provided. Stay tuned!

