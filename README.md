# majaro_KDE_asus_X205TA

1. Download a 64bit Manjaro distro: have not tested Ubuntu.

2. Used gparted to format a usb to fat32 and labeled the media.
   Use UNetbootin to flash Manjaro for a writable boot-media.

3. Get a i386-efi folder from a 32-bit arch linux distro.
   Paste it into /boot/grub/

4. Copy the grubia32.efi to the folder /manjaro/


5. in kernels.cfg change:
   misolabel= insert_label_of_media here
 
6. in grub.cfg change a line in function efi_detect to:
   for efi in (*,gpt*)/efi/*/*.efi (*,gpt*)/efi/*/*/*.efi (*,gpt*)/*.efi (*,gpt*)/*/*.efi (*,msdos*)/*/*/*.efi ; do

7. in F2 menu select USB Controller Select to EHCI and Disable secure boot.

8. Boot override to the live media.

9. Before starting calamares from the live-usb session modify the /usr/lib/calamares/modules/bootloader/main.py file and change this line to:
   check_target_env_call(...[grubinstall] --target ... , "--no-nvram", "removable"])

Install from calamares.
If it gives you an error, don't exit. To install grub on uefi 32 bit, open terminal and type

10. sudo grub-install --target=i386-efi --efi-directory=/boot/efi --bootloader-id=Manjaro --force
If an error occurs run the command again.

