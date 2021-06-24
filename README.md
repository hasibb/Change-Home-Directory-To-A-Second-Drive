Move Your Home Directory To A Second Drive
By Hasib



Make Reinstalling Faster By Having Home On A Second Drive


Note: You may want to drop into tty to perform the following to avoid any weird side effects from doing this within your graphical environment. Also, for this example we will assume that your partition is sdb1 (change this to the id of your drive!). Also, have a backup.



Mount the new partition to /tmp:

sudo mkdir /mnt/tmp
sudo mount /dev/sdb1 /mnt/tmp


Copy your HOME content to the second drive:

sudo rsync -avx /home/ /mnt/tmp


Mount our new HOME partition:

sudo mount /dev/sdb1 /home


If all your data seems to be present on the second drive and new partition, you may delete your old /home directory. To do this, you must first unmount the new /home partition!

sudo umount /home #unmount the new home first!


Then you may delete the original /home:

rm -rf /home/*


Now let's make your new /home permanent. Get the UUID so we can add it to your fstab:

sudo blkid


Then edit the fstab:

sudo vim /etc/fstab #or nano if you prefer


Add this line at the end of the fstab:

UUID=<noted number from above> /home ext4 defaults 0 2


Now reboot and see if it works!

sudo reboot
  
#____Hopefully, it will work properly____#
