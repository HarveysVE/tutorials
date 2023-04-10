# Hackintosh Starter Guide 2023
In this video Harvey will show you how to get started with Hackintosh. From choosing parts, Preparing your Hypervisor to actually installing you macOS Monterey Hackintosh and getting everything working. <br>

Video Link: https://youtu.be/U8cN7dEVG_8 <br>

Commands used in this video: <br>
<br>
Desktop GUI Commands: <br>

```
apt-get update && apt-get dist-upgrade
```

```
apt-get install xfce4 chromium lightdm -y
```

```
adduser proxmox
```

```
systemctl start lightdm
```

<br>
Hackintosh Monterey VM Creation Commands: <br>
<br>
For Intel CPU's

```
args: -device isa-applesmc,osk="ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -cpu host,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc
```

<br>
For AMD CPU's : <br>

```
args: -device isa-applesmc,osk=\"ourhardworkbythesewordsguardedpleasedontsteal(c)AppleComputerInc\" -smbios type=2 -device usb-kbd,bus=ehci.0,port=2 -global nec-usb-xhci.msi=off -cpu Penryn,kvm=on,vendor=GenuineIntel,+kvm_pv_unhalt,+kvm_pv_eoi,+hypervisor,+invtsc,+pcid,+ssse3,+sse4.2,+popcnt,+avx,+avx2,+aes,+fma,+fma4,+bmi1,+bmi2,+xsave,+xsaveopt,check
```

Download Links for Monterey VM Creation: <br>

macOS ISO Download Link: https://archive.org/details/macos-collection <br>

Clover Configurator Download: https://mackie100projects.altervista.org/download-clover-configurator/ <br>

Opencore Configurator: https://mackie100projects.altervista.org/opencore-configurator/ <br>

Opencore ISO : https://github.com/thenickdude/KVM-Opencore/releases <br>

You have successfully setup Hackintosh the new way. Congratulations! <br>

Hope you enjoyed this video if you did, please consider subscribing and also leave a like so I know to do more Hackintosh videos in the future. Thanks ever so much for watching goodbye.