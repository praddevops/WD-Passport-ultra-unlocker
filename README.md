###### mirrored from https://github.com/geekhaidar/WD-Passport-Unlock-Linux.git

## Unlocking WD Passport Ultra Hard Disk  on Linux/ Ubuntu Operating System

Follow the steps below to unlock the WD HDD originally locked by the WD Security Software:

1. Open Terminal and type the following command: `dmesg | grep -i scsi`
   This will provide your WD Passport drive name
   
   ![image](https://github.com/praddevops/WD-Passport-ultra-unlocker/assets/7948650/55a04f5c-f945-4a62-adf1-2020d5a970a2)

   
   Example : In my case its "sda" - See the line `[sda] Attached SCSI disk` (Third line from the bottom in the image above)
2. Clone the repo in your `$HOME` folder
3. Type the following in the terminal :
   ```
    cd ~/WD-Passport-ultra-unlocker
    chmod u+x cookpw.py
    ./cookpw.py THEPASSWORD > password.bin
    ```
  (Note: Enter your Password instead of THEPASSWORD. You may have to do this step twice if you get an error after first time)
  
4. Install 'sg3_utils' package for your distro depends on the distro you use !
*   Example for debian :
*   http://sg.danny.cz/sg/sg3_utils.html
*   Then go to Download and Build 
*   Then scroll down to download 1.42 --- sg3-utils_1.42-0.1_i386.deb (for 32 bit system) or sg3-utils_1.42-0.1_amd64.deb (for 64 bit system) and install it by just opening it.
*  In case link expires download sg_utils it from the following github link -- https://github.com/geekhaidar/sg3_utils_WD

  On ubuntu, you can download sg3-utils with apt-get
```
sudo apt-get update -y
sudo apt-get install -y sg3-utils
```
5. Run the following in the terminal `sudo sg_raw -s 40 -i password.bin /dev/sda c1 e1 00 00 00 00 00 00 28 00`
*   (Note : Instead of "sda" enter the name of your WD as acquired in Step 1)
*   If prompted, enter your password
8. You will get an output : `SCSI Status : Good` if unlocking process is successful
   
### Accessing the disk:

1. Create a Directory
       `sudo mkdir ~/media`
2. Use `lsblk` or `lsblk -f` to find the partition name (in my case it's sda1)
   ![image](https://github.com/praddevops/WD-Passport-ultra-unlocker/assets/7948650/67359b34-614c-455b-8972-10dc441baaa2)

3. Mount the volume
       `sudo mount /dev/sda1 ~/media`
4. Your WD HDD is now accessible from `~/media` folder
5. Unmount the HDD by executing the following command `sudo umount /dev/sda1` before unplugging the HDD  
