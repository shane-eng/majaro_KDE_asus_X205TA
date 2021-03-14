# majaro_KDE_asus_X205TA
Use UNetbootin for a writable boot-media.

in kernels.cfg change:

misolabel=<insert label of media here>
 
in grub.cfg change a line in function efi_detect to:

for efi in (*,gpt*)/efi/*/*.efi (*,gpt*)/efi/*/*/*.efi (*,gpt*)/*.efi (*,gpt*)/*/*.efi (*,msdos*)/*/*/*.efi ; do

