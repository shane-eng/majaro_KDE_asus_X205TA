# majaro_KDE_asus_X205TA
Thank you. Following instructions from https://gist.github.com/GeoffreyCoulaud/074d2c4495578c0602f6180bc1a2e6eb

1. Download a 64bit Manjaro distro: have not tested Ubuntu.

2. Used gparted to format a usb to fat32 and label the media.
   Use UNetbootin to flash Manjaro for a writable boot-media.

3. Get a i386-efi folder from a 32-bit arch linux distro.
   Paste it into /boot/grub/

4. Copy the grubia32.efi file to the folder /manjaro/ on the stick

5. Copy the bootia32.efi file to the folder /efi/boot/ on the stick

6. in /boot/grub/kernels.cfg change:
   misolabel= insert_label_of_media_here
 
7. in /boot/grub/grub.cfg change a line in function efi_detect to:
   for efi in (*,gpt*)/efi/*/*.efi (*,gpt*)/efi/*/*/*.efi (*,gpt*)/*.efi (*,gpt*)/*/*.efi (*,msdos*)/*/*/*.efi ; do

8. in F2 menu select USB Controller Select to EHCI and Disable secure boot.

9. Boot override to the live media.

10. Before starting calamares from the live-usb session modify the /usr/lib/calamares/modules/bootloader/main.py file and change this line to:
   check_target_env_call(...[grubinstall] --target ... , "--no-nvram", "--removable"])

Install from calamares.
If it gives you an error, don't exit. To install grub on uefi 32 bit, open terminal and type:

11. sudo grub-install --target=i386-efi --efi-directory=/boot/efi --bootloader-id=Manjaro --force

If an error occurs run the command again.
Boot normally without live-usb

Wifi


