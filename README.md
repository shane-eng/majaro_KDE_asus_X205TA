# majaro_KDE_asus_X205TA
Thank you. Following instructions from https://gist.github.com/GeoffreyCoulaud/074d2c4495578c0602f6180bc1a2e6eb

1. Download a 64bit Manjaro distro: have not tested Ubuntu.

2. Used gparted to format a usb to fat32 and label the media.
   Use UNetbootin to flash Manjaro for a writable boot-media.

3. Get a i386-efi folder from a 32-bit arch linux distro.
   Paste it into /boot/grub/

4. Copy the grubia32.efi file to the folder /manjaro/ on the stick: I got mine from http://ftp.scientificlinux.org/linux/scientific/7/x86_64/os/EFI/BOOT/

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
If it gives you an error, don't turn off yet. To install grub on uefi 32 bit, open terminal and type:

11. sudo grub-install --target=i386-efi --efi-directory=/boot/efi --bootloader-id=Manjaro --force

If an error occurs run the command again.
Boot normally without live-usb.

# Get Wifi working.

From harryharryharry on ubuntu forums getting linux to work on X205TA.
https://ubuntuforums.org/archive/index.php/t-2379657.html

Use brcmfmac43340-sdio.txt from
https://raw.githubusercontent.com/harryharryharry/x205ta-iso2usb-files/master/brcmfmac43340-sdio.txt
which has the added benefit of supporting 5GHz networks (pretty weird the version in the EFI variables doesn’t...)

2. How to gain internet connectivity
The internal wireless card’s module (brcmfmac) needs a file called /lib/firmware/brcm/brcmfmac43340-sdio.txt to get the card up and running, but it’s missing (well it’s not in the right location). You can copy it by running the following commands:

# probably not necessary, but to be sure the EFI variables are properly exposed to userspace
sudo modprobe efivarfs
sudo mount -t efivarfs efivarfs /sys/firmware/efi/efivars

# then copy the file that starts with nvram to /lib/firmware/brcm
sudo cp -a /sys/firmware/efi/efivars/nvram* /lib/firmware/brcm/brcmfmac43340-sdio.txt

# and reload the brcmfmac module
sudo rmmod brcmfmac
sudo modprobe brcmfmac


