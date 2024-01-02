# expand_diskSize_vsphere

Extending the Logical Volume ubuntu--vg-ubuntu--lv to Use the Entire 60GB Disk

Prerequisites:

Root access to the virtual machine
The virtual disk has already been extended to 60GB in vSphere
Steps
Resize the Physical Volume (PV):

```
pvresize /dev/sda3
```
Use code with caution. Learn more
Extend the Logical Volume (LV):

```
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```

Use code with caution. Learn more
Resize the Filesystem:

```
resize2fs /dev/ubuntu-vg/ubuntu-lv
```
Use code with caution. Learn more

Additional Notes:

Replace /dev/sda3 with the correct path to your physical volume if it differs.

If you encounter any errors, consult the documentation for lvm and your filesystem for troubleshooting guidance.
For more detailed explanations of each step, refer to the LVM documentation or online resources.
Verification
After completing these steps, use the lvs command to verify that the logical volume has been extended to the full size of the disk. 



# IF need to add sda4

Here are the steps:

Create a New Partition:

Use the fdisk tool to create a new partition in the unallocated space:
```
fdisk /dev/sda
Within fdisk:
Press n to create a new partition.
Choose p for a primary partition.
Select partition number 4 (as /dev/sda1, /dev/sda2, and /dev/sda3 already exist).
Accept the default first sector (which will use all available unallocated space).
Press w to write the changes to disk.
```
Verify Partition Creation:

Use `lsblk -l` to confirm that /dev/sda4 now exists:

```
lsblk -l
```

Use code with caution. Learn more
Extend Volume Group:

Now that /dev/sda4 exists, retry extending the VG:
```
vgextend ubuntu-vg /dev/sda4
```
Verify VG Size:

Use vgdisplay to check if the VG size has increased:
```
vgdisplay
```

```
lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
```

```
resize2fs /dev/ubuntu-vg/ubuntu-lv
```

```
lsblk -l
df -h
```
