# Installing and Configuring AMD Diagnostics on Ubuntu

##Revision History

Rev 1.00 (December 10, 2016)

* Initial release.

## 1. Introduction
This document describes how to install and configure AMD diagnostics tools that are intended for the testing of AMD graphics products. AMD diagnostics tools are required to be run on a Linux®-based operating system, such as Ubuntu.
Please contact your AMD Field Applications Engineer or technical representative with any questions about this document.

## 2. Installing and Configuring AMD Diagnostics
1. Startupyoursystem.Ifneeded,pressCtrl+Alt+F1toswitchfromGUImode (shown below) to text mode.![1](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/1.png)

2. Provide your credentials as required.![2](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/2.png)

3. Type sudo passwd root to change the root password (and to enable the root user account).![3](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/3.png)

4. Type su - to switch to the root user.

	Note: All steps from this point must be carried out by the root user. If the system restarts, log on to the system as the root user as shown below.![4](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/4.png)

5. (Optional) Enable automatic login as the root user by doing the following:
  * a. Type sudo pico /etc/init/tty1.conf and edit the line exec /sbin/getty -8
38400 tty1 to read /sbin/getty -a root -8 38400 tty1.
Press Ctrl + X to exit the file and press Y when prompted to save your
changes.
  * b. Type pico /etc/lighdm/lightdm.conf and add greeter-show-manual-
login=true to the end of the file.
Press Ctrl + X to exit the file and press Y when prompted to save your
changes.

6. Install the AMD diagnostics tools and set up the test environment as required:
  * a. Download the setup_client.sh script from the Partner ORC at http:// secure.amd.com using the wget command (i.e., wget [Web_address_of_script]).
  
  * b. Type chmod 777 setup_client.sh to make the script executable.

  * c. Type ./setup_client.sh to install the tools.![5](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/5.png)

  You can also use the following commands for installation.
  
  Table 2–1 Additional Installation Commands![6](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/6.png)
  
  
7. Type nano /etc/default/grub to edit the grub configuration file and:
       
  * a.Add # before GRUB_HIDDEN_TIMEOUT=0.
  * Add text mem=1024M iommu=off efi=old_map consoleblank=0 to GRUB_CMDLINE_LINUX_DEFAULT and GRUB_CMDLINE_LINUX. 
  * Press Ctrl + X to exit the file and Y when prompted to save your changes.![7](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/7.png)
  
  Note: The recommended system memory for diagnostics is at least 2 GB for mem=1024M.
  
8. Type update-grub to update your settings.

9. Configure SSH to allow its use in root user mode and to prevent it from timing out too quickly:
  * a. Type nano /etc/ssh/sshd_config, add # before PermitRootLogin without-password, change the StrictModes setting to no, and reboot your system by typing reboot.![8](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/8.png)
  * b. To prevent the SSH client from timing out, type nano /etc/ssh/ ssh_config, add # before Keep SSH Session From Disconnecting, add ServerAliveInterval 60, and reboot your system.![9](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/9.png)

10. Add the following modules/drivers to the black list. This is required for compatibility with AMD Diagnostics tools.
  * a. Type nano /etc/modprobe.d/blacklist-framebuffer.conf.
  * b. Make sure the following lines appear in the file:
  blacklist fbcon![10](https://raw.githubusercontent.com/auspbro/configuring-linux-script-autorun/master/res/10.png)
  
                      blacklist vga16fb
                      blacklist radeon
                      blacklist snd
                      blacklist snd_hda_codec
                      blacklist snd_hda_codec_hdmi
                      blacklist snd_hwdep
                      blacklist snd_page_alloc
                      blacklist snd_pcm
                      blacklist snd_rawmidi
                      blacklist snd_seq
                      blacklist snd_seq_device
                      blacklist snd_seq_midi
                      blacklist snd_seq_midi_event
                      blacklist snd_timer soundcore
                      blacklist snd_hda_intel
                      blacklist shpchp
                      
   * c. Press Ctrl + X to exit the file and Y when prompted to save your changes.
  
  

  
