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
