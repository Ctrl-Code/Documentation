# GRUB-NOT-INSTALLING

This issue is related to the installation of `grub installations` in pc or notebooks where you

1. Install Windows
2. Install Ubuntu

# EXPECTED OUTCOME

*grub* appears

# UNEXPECTED OUTCOME

**Windows** boot up and **no** grub menu.

# FIX

1. **BACKUP** `/boot/efi/EFI` in Some other Drive or some other media so that if anything goes wrong you do not have other troubles and the fix can be done by **RESTORING** the backup through some live-boot installations. The size would be around 10MB - 15MB.
2. [Copying](##copying) - `grubx64.efi`
3. [Installing](##installing) - `grub-customizer`
4. [Editing](##editing) - `windows bootentry`

## Copying

1. Copy *`grubx64.efi`* file from `/boot/efi/EFI/ubuntu` and paste into `/boot/efi/EFI/Microsoft/Boot`.
2. Rename file *`bootmgfw.efi`* in `/boot/efi/EFI/Microsoft/Boot` to *`windows.efi`*
3. Rename *`grubx64.efi`* file in `/boot/efi/EFI/Microsoft/Boot` to *`bootmgfw.efi`*

## Installing

Install `grub-customizer` from [site's link](https://launchpad.net/~danielrichter2007/+archive/ubuntu/grub-customizer)

## Editing

1. Run `grub-customizer`.
2. Edit the windows boot entry in it such that it shows *`Boot sequence`* and last line of the code as `bootmgfw.efi` in the path of *chailoader* by making it  ~~`bootmgfw.efi.`~~ `windows.efi`