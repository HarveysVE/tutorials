# Proxmox Clustering Introduction
<br>
In this video Harvey shows you the basics of Proxmox Clustering. How to create a cluster, setup shared storage and Configure High Availability (HA). Hope you enjoy! <br>
<br>
Video Link : https://youtu.be/q6r_2my-Py4 <br>
Samba Server Install Commands: <br>

```
sudo apt-get update
sudo apt-get upgrade
```

```
sudo apt-get install samba samba-common-bin
```

```
mkdir /mnt/vm
```

```
sudo nano /etc/samba/smb.conf
```

```
[nameofshare]
path = /mnt/vm
writeable=Yes
create mask=0777
directory mask=0777
public=no
```

```
adduser proxmox
```

```
sudo smbpasswd -a proxmox
```

```
chmod 0777 /mnt/vm
```

```
sudo systemctl restart smbd
```
