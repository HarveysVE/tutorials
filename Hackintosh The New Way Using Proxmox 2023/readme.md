# Hackintosh The New Way Using Proxmox 2023
<br>
In this video Harvey shows you how to setup Hackintosh The New Way. Using Proxmox a type 1 hypervisor. This guide includes : Proxmox Installation, macOS VM Creation and GPU Passthrough. Hope you enjoyed watching this video! If you did a like and maybe a subscribe would be greatly appreciated. <br>
<br>
Video Link : https://youtu.be/QFlhSOypPaw <br>
Download Links: <br>
Proxmox ISO Download : https://proxmox.com/downloads <br>

BalenaEtcher Download : https://www.balena.io/etcher <br>

OpenCore Bootloader ISO Download: https://github.com/thenickdude/KVM-Opencore/releases <br>

macOS ISO Download : https://archive.org/details/macos-collection <br>
<br>
Arguments used in installation: <br>
Intel CPUs: <br>
```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```
<br>
AMD CPUs: <br>

```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -cpu Penryn,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc,+pcid,+ssse3,+sse4.2,+popcnt,+avx,+avx2,+aes,+fma,+fma4,+bmi1,+bmi2,+xsave,+xsaveopt,check
```
<br>
