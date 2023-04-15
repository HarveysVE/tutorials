# How to Install Hackintosh The New Way Using Proxmox In Depth Guide
In this video Harvey shows you in depth how to install Hackintosh The New Way Using Proxmox. And also installs Windows 11 and runs it at the same time alongside macOS. This video also includes benchmarks of both Windows 11 and macOS. With some of the benchmarks running at the exact same time as eachother. Hope you like the video as this video did take a long time to make but if you did like it please leave a like and consider pressing that subscribe button. Thanks for watching! <br>
<br>
Links / Commands : <br>
<br>
Proxmox ISO Download : https://proxmox.com
<br>
Balena Etcher Download : https://balena.io/etcher
Opencore ISO Download : Download from above /\
macOS ISO Download (Download as torrent) : https://archive.org/details/macos-collection
<br>
<br>
Expand Local Volume Commands : <br>
<br>
Delete the 'Local-LVM' Volume from the Web GUI like shown in the video. <br>
<br>
Run these commands in the proxmox shell : <br>

```
lvremove /dev/pve/data
```
<br>

```
lvresize -l +100%FREE /dev/pve/root
```
<br>

```
resize2fs /dev/mapper/pve-root
```
<br>
GPU Passthrough Commands <br>
<br>
Preparing your grub boot loader and enabling IOMMU <br>

Open up the grub configuration file using the command below:
```
nano /etc/default/grub
```
Then, enter the corresponding arguments according to your system:

For Intel CPUs:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt video=vesafb:off video=efifb:off"
```
For AMD CPUs:
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on iommu=pt video=vesafb:off video=efifb:off"
```
Then update grub using the following command: <br>
```
update-grub
```
Now reboot using the following command:
```
reset
```
Once the Proxmox Node has rebooted run the following command to see if IOMMU is enabled:
```
dmesg | grep -e DMAR -e IOMMU
```
<br /> If everything is working you should see a message that tells you that IOMMU is enabled. Now we are ready to move on to the next part

Now we are going to add the required modules to a configuration file so that PCI-E passthrough will work using the following commands:

First use the command below to edit the modules file: <br />
```
nano /etc/modules
```
<br>
Then place the following into the file: 
<br />

```
vfio
vfio_iommu_type1
vfio_pci
vfio_virqfd
```
<br>
Once this has done save the file using ctrl x then y and press enter to save.
<br>
We are next going to see if our system supports IOMMU Remapping using the following command: <br>

```
dmesg | grep 'remapping'
```
<br>
Fixing Unable To Get Tail (Got 0 Bytes) : <br>
<br>
NOTE : The only fix for getting AMD GPUs to work in proxmox is downgrading the kernel by doing the following <br>
Credit : ar2r <br>
<br>
To downgrade to the working kernel 

<br>
I did following steps: 

#if you don’t have enterprise subscription of proxmox I suggest to remove it from repository as it’s annoying to get those messages when you do apt update in shell login to your web browser to proxmox, go to your main node, and go to REPOSITORY tab. <br>
Remove enterprise repository and add following non-subscription repository: 
<br>
http://download.proxmox.com/debian/pve bullseye pve-no-subscription
<br>
<br>
after that go to your main node 
Shell and execute following commands: <br>
<br>

````
apt update
````

```
apt install pve-kernel-5.15.53-1-pve
```
```
proxmox-boot-tool kernel pin 5.15.53-1-pve
```
```
reboot now
```

After that you your proxmox will ask you on the boot screen what kernel you would like to use. So choose 5.15.53-1-pve
After that when you run your mac VM you shouldn’t have that tail error anymore.
<br>
<br>
macOS Virtual Machine Creation Commands : <br>
<br>
If you are using an Intel CPU use these arguments : <br>

```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```

If you are using an AMD Ryzen CPU use these arguments : <br>

```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -global ICH9-LPC.acpi-pci-hotplug-with-bridge-support=off -cpu Haswell-noTSX,vendor=GenuineIntel,+invtsc,+hypervisor,kvm=on,vmware-cpuid-freq=on
```

<br>

Sharemouse Download Link : https://sharemouse.com
