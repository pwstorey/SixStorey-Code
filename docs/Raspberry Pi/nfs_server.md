# How to set-up an NFS server on raspberry pi 

## How to mount an external drive 

First we need to make a directory to mount the drive 

```bash 
sudo mkdir -p /opt/nfs
```

Then we need the drive to automatically mount when the pi boots. We can either link the drive via it's path like /dev/sda1 for example or we can use the partition ID of the drive. To get the partition ID we use the following command: 

```bash
sudo lsblk
sudo blkid /dev/sda1
```

No we edit the /etc/fstab file adding a line to mount this drive. 

```bash 
sudo nano /etc/fstab
```

Adding the lines for example: 

```bash 
/dev/sda1 /opt/nfs defaults,user 0 1 

OR

PARTUUID=<enter the partition id here> /opt/nfs ext4 defaults,noatime,nodiratime 0 2 
```

save and quit. Then we can reboot to mount the drive automatically or we can mount the drive manually this time to save some time. 

```bash 
sudo mount /opt/nfs
ls /opt/nfs
```


## Install the NFS Server 

We can install the NFS server with the command: 

```bash 
sudo apt install -y nfs-kernel-server 
```

Next we edit the /etc/exports file to export (share) the folder on the network. 

```bash 
/opt/nfs *(rw,sync,no_subtree_check)
OR
/opt/nfs 192.168.50.0/24(rw,sync)
```

In the first example the * represents all IP addresses, i.e. everyone, in the second example, we are exporting it to 192.168.50.0/24 which is shorthand for "all the IP addresses between 192.168.50.0 and 192.168.50.254".

