
>#	Probleum Description
A probleum occured when I deleted an entry of windows 10 bootloader while deleting some redundant entries by using a software named 'easyefi.exe' (available on windows platform only). After this I was unable to load the windows kernel. I did this out of curiosity though !

>#	System Configuration
I am using an HP laptop, with dual booted UBUNTU 18.04 and WINDOWS 10 os.


	NOTE: The softwares 'easybcd' and 'easyefi' provides an easy inerface to boot configuration. 'easybcd' software was used at the time of traditional BIOS and MBR approach whereas many new computers after windows 8,10 are being shipped with a modern UEFI firmware and boot manager replacing the traditional BIOS and MBR approach. Since I am using windows 10, i.e. why I installed 'easyefi' to do so.


>##	FIRST APPROACH
When I first started ON my HP laptop, I got a "please wait" prompt before loading windows 10. From this I figured out about the windows HDD boot entry ('bootx86.efi' which is a copy of 'bootmgfw.efi') kept at the location `/boot/efi/EFI/Microsoft/bootmgfw.efi`. At the location	`/boot/efi/EFI/Microsoft`, just copy the `grubx64.efi` (which is the grub bootloader itself). So, I tried making entries of windows OS manually in the file named `40_custom` present in directory `/etc/grub.d/`


>##	CUSTOM MENU ENTRIES IN GRUB ("/etc/grub.d/40_custom")
The scripts stored in the directory "grub.d" are the scripts that executes when grub program starts. In the file '40_custom' we can add custom boot menu entries for grub. After writing entries to this file, update grub by issuing a command as superuser..

```	
$ sudo update-grub
```


>##	GRUB CONFIGURATION ("/etc/default/grub")
I then got to know about the GRUB CONFIG FILE in "/etc/default/grub", in which we can modify various features of grub including color scheme, timeout, background, setting passwords and much more.
	

>##	ADDITIONAL INFORMATION (GRUB BOOTLOADER)
* The grub bootloader (grubx64.exe) is stored in the directory "/boot/efi/EFI/ubuntu" when grub in installed via ubuntu setup. On systems with "secure boot" active, 'grubx64.efi' won't boot, so there is another program in this directory named 'shimx64.efi' which solves this issue by adding its own security tools and registering itself with the firmware. It launches the 'grubx64.exe' present in its directory.

	NOTE : MAC does not support secure boot launching 'shimx64.efi' is similar to launching 'grubx64.efi'. Also if you want to start a different bootloader instead of grub, for example 'windows bootmgr' you will need to keep it in the directory of 'shimx64.efi' by the name of 'grubx64.efi' since shim is configured to launch the bootloader by the name of 'grubx64.efi'.
			 

*	SECOND APPROACH
After I tried playing with grub and manually adding entries to grub in hope
	that my WINDOWS 10 OS would load, it did not work out. Maybe my efi
	bootloader needed some repairing or I guess it was'nt able to either find 
	out the boot code for WINDOWS os or maybe the boot code got corrupted 
	somehow. With all of these things running in my mind, 
	I entered the advance options for troubleshooting using command prompt, 
	and thought though of generating another EFI bootloader (i.e. 'bootx64.efi')
	I did this by issuing the bellow command for boot recovery in CMD console
	provided to me for troubleshooting.
	NOTE : Before issuing the commands, just change the directory to 'C:'. So
		   that it does not give us the error prompt - "could not find 
		   the location specified", while issuing the last command.
```
		> C:
		> bootrec.exe /ScanOS
		> bootrec.exe /fixmbr
		> bootrec.exe /fixboot 			(access denied)
		> bootrec.exe /RebuildBcd		(this worked)
```

This last option `/RebuildBcd` scans for all disks for installation of an operating system compatible with windows Vista/7. It lets us select the installation we want to add to the 'BCD Store' (explained bellow). 

>##	BCD STORE
A BCD store has one or more instances of the "Windows boot loader". A separate BCD object represents each instance. Each instance loads one of the installed versions of windows having configuration as specified by the object's environment.


>##	EFIBOOTMGR (UBUNTU)
This command line tool is used to manipulate the EFI Boot Manager on linux platform.


>##  MANAGE WINDOWS BOOTLOADER OPTIONS  
Console utility `bcdedit.exe` intended to manage all the options of modern windows bootloader. This can be used if your windows 10 os is loaded.


>### Author : `Abhinav Thakur`
>### Email  : `compilepeace@gmail.com`  
>### Date   : `May 30, 2018`

