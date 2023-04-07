# High Sierra The New Way (Not Finished! Don't follow without the video)
Welcome to the new way first of all. 
This document will include everything you need to get High Sierra Working the new way. Including GPU Passthrough.

Because High Sierra Natively Supports NVIDIA GPUs we don't need any special patches which is great! <br /> 
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
Opencore V19 ISO File : Download from above <br />
High Sierra ISO Download (Torrent) : Download Magnet File From Above /\ <br />
<br />
Thats all you need! <br>