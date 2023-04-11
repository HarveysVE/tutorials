# High Sierra The New Way (Not Finished!)
Welcome to the new way first of all. 
This document will include everything you need to get High Sierra Working the new way. Including GPU Passthrough.
(This Guide Assumes You Already Have Enabled IOMMU In The BIOS And In Proxmox. If your Unsure On How To Enable IOMMU Join My Discord)
Because High Sierra Natively Supports Most NVIDIA GPUs we don't need any special patches which is great! All you need to do is pass the gpu through. <br /> 
You do need boot arguments to make macOS boot on proxmox which you can find below (Remember to use the ones relating to your CPU)<br> 
<br>
Intel CPUs:
```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```
AMD CPUs:
```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -cpu Penryn,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc,+pcid,+ssse3,+sse4.2,+popcnt,+avx,+avx2,+aes,+fma,+fma4,+bmi1,+bmi2,+xsave,+xsaveopt,check
```
Download Links: <br>
Opencore V19 ISO File : Download ISO from above <br />
High Sierra ISO Download (Torrent) : Download Torrent File From Above /\ <br />
<br />
Thats all you need! <br>