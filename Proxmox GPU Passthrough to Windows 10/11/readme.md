# Proxmox GPU Passthrough to Windows 10/11
<br>
In this video Harvey shows you how to passthrough a GPU to a Windows 10 or 11 virtual machine, with tests, benchmarks, gaming and much more. <br>
Video Link : https://www.youtube.com/watch?v=ecFtSFCJqSg <br>
<br>
Commands used in this video: <br>
Preparing your grub boot loader and enabling IOMMU <br>
Open up the grub configuration file using the command below: <br>

```
nano /etc/default/grub
```
Then, enter the corresponding arguments according to your system: <br>
For Intel CPUs: <br>
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt video=vesafb:off video=efifb:off"
```
<br>
For AMD CPUs: <br>

```
GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on iommu=pt video=vesafb:off video=efifb:off"
```
Then update grub using the following command: <br>
```
update-grub
```

Now reboot using the following command: <br>
```
reboot
```
<br>
Once the Proxmox Node has rebooted run the following command to see if IOMMU is enabled: <br>

```
dmesg | grep -e DMAR -e IOMMU
```
<br>
If everything is working you should see a message that tells you that IOMMU is enabled. Now we are ready to move on to the next part <br>

Now we are going to add the required modules to a configuration file so that PCI-E passthrough will work using the following commands: <br>

First use the command below to edit the modules file: <br>

```
nano /etc/modules
```
Then place the following into the file: <br>

```
vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd
```

Once this has done save the file using ctrl x then y and press enter to save.

We are next going to see if our system supports IOMMU Remapping using the following command: <br>

```
dmesg | grep 'remapping'
```
If you see one of the lines below then your system supports it:

"AMD-Vi: Interrupt remapping enabled" 

"DMAR-IR: Enabled IRQ remapping in x2apic mode

<br>
If you do not see any of the following messages no worries! Fix it by putting the following command into the command line: <br>

```
echo "options vfio_iommu_type1 allow_unsafe_interrupts=1" > /etc/modprobe.d/iommu_unsafe_interrupts.conf
```
Thats it! Now passthrough the GPU to see if it works. If your unsure how to do this watch the video on how I do it at the top of this post. <br>