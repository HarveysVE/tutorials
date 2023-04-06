# Hackintosh Ventura The New Way
Proxmox ISO Download : https://proxmox.com/downloads

BalenaEtcher Download : https://www.balena.io/etcher

OpenCore Bootloader ISO Download: https://github.com/thenickdude/KVM-Opencore/releases

macOS ISO Download : https://archive.org/details/macos-collection

Arguments used in installation:

Intel CPUs:

args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
<br / >
AMD CPUs:

args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -cpu Penryn,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc,+pcid,+ssse3,+sse4.2,+popcnt,+avx,+avx2,+aes,+fma,+fma4,+bmi1,+bmi2,+xsave,+xsaveopt,check
GPU Passthrough Commands
Preparing your grub boot loader and enabling IOMMU

Open up the grub configuration file using the command below:

nano /etc/default/grub <br />
Then, enter the corresponding arguments according to your system:

For Intel CPUs:

GRUB_CMDLINE_LINUX_DEFAULT="quiet intel_iommu=on iommu=pt video=vesafb:off video=efifb:off" <br />

For AMD CPUs:

GRUB_CMDLINE_LINUX_DEFAULT="quiet amd_iommu=on iommu=pt video=vesafb:off video=efifb:off" <br />
Then update grub using the following command:

update-grub </br>
Now reboot using the following command:

reset <br />
<br />
Once the Proxmox Node has rebooted run the following command to see if IOMMU is enabled:

dmesg | grep -e DMAR -e IOMMU <br />
<br /> If everything is working you should see a message that tells you that IOMMU is enabled. Now we are ready to move on to the next part

Now we are going to add the required modules to a configuration file so that PCI-E passthrough will work using the following commands:

First use the command below to edit the modules file: <br />

nano /etc/modules <br />
<br>
Then place the following into the file: <br />
<br>
vfio <br>
vfio_iommu_type1 <br>
vfio_pci <br>
vfio_virqfd <br>
<br>
Once this has done save the file using ctrl x then y and press enter to save.
<br>
We are next going to see if our system supports IOMMU Remapping using the following command: <br>
<br>
dmesg | grep 'remapping'
<br>
<br>If you see one of the lines below then your system supports it: <br>

“AMD-Vi: Interrupt remapping enabled”
“DMAR-IR: Enabled IRQ remapping in x2apic mode <br>
<br>If you do not see any of the following messages no worries! Fix it by putting the following command into the command line: <br>
<br>
echo "options vfio_iommu_type1 allow_unsafe_interrupts=1" > /etc/modprobe.d/iommu_unsafe_interrupts.conf <br>