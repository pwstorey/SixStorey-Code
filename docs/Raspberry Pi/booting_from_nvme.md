# How to set-up and boot a Raspberry Pi from an NVMe SSD 

## Firmware

Make sure your Raspberry Pi 5 firmware is up to date with the 2023-12-06 or later version. A software update on the RPi OS should do this for you, but you can force it by running: 

```bash
sudo rpi-eeprom-update 
```

in the Terminal. This will also tell you which firmware is running. 

## Power 

The NVMe hat uses around 5W of power but worth monitoring power usage SSD so that you don't have any isues.  

## Set-up

List Block Devices - ususally wont show the NVMe device without it being configured. 
```bash 
lsblk
```
We need to edit the configuration files to access our NVMe SSD. 
```bash 
sudo nano /boot/config.txt
```

At the very end after [all] we add the lines: 

```bash 
[all]
dtparam=nvme
dtparam=pciex1_gen=2 
```
Gen 2 is supported but Gen 3 seems to be stable and 
Ctrl-X to save and exit, sudo reboot. Trying lsblk again and we can check to see if we can see the NVMe drive. 

 
## PCIe 3 Mode

To enable experimental and not-officially-supported PCIe 3 mode, add the follow line to the [all] section at the end of your Raspberry Pi /boot/config.txt file:

```bash
[all]
dtparam=pciex1_gen=3
```

## Speed Testing 

We can test the speed of the drive using the name of the ssd drive from the lsblk command: 

```bash 
sudo hdparm -t --direct /dev/nvme0n1
```


## How to boot from the NVMe SSD 

First of all fully update the pi and reboot: 

```bash
sudo apt update 
sudo apt upgrade 
sudo reboot 
```

We can edit the EEPROM configuration files with: 

```bash 
sudo rpi-eeprom-config --edit
```

Change the BOOT_ORDER line to the following:
```bash 
BOOT_ORDER=0xf416
```

The 6 represents the NVMe SSD drive. Then add the following line if using a non-HAT+ adapter:
```bash 
PCIE_PROBE=1
```