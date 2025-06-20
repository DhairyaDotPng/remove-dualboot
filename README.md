## Completely remove your Linux Distro in Dual-Boot
Just deleting the linux partition is not enough to completely remove linux from your dual boot configuration, there are a few leftovers even after deleting the volume that can be removed for a cleaner system
### Deleting Partitions
1. Open disk management in windows
2. Delete linux volume
3. Delete linux boot volume (around 1 GiB Healthy Partition)
### Deleting Boot Config Entry
1. Open cmd as admin
2. `bcedit /enum firmware`
3. Identify linux entry via description
4. Copy its identifier for eg: `{0de667f3-4d55-11f0-b03f-806e6f6e6963}`
5. `bcdedit /delete {identifier}`
### Deleting Grub entry from EFI
1. Open cmd as admin
2. Use diskpart via: `diskpart`
3. List the disks via: `list disk`
4. Select disk where efi is located for eg: `select disk 0`
5. List the volumes via: `list vol`
6. Select the EFI volume, mostly FAT32 and labelled as System under Info (Verify via disk management, should say Healthy (EFI system partition)) for eg: `select volume 2`
7. Assign an unused letter to the volume via: `assign LETTER=Z:`
8. Exit diskpart via: `exit`
9. Go to EFI volume via: `Z:`
10. Go to linux folder for eg: `cd fedora`
11. Make sure it contains grub.cfg file via: `dir`
12. Go back one folder via: `cd ..`
13. Delete the linux folder via: `rmdir /s fedora`
14. Type in `y` for confirmation
15. Reboot
