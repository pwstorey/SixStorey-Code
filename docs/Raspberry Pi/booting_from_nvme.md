# How to set-up and boot a Raspberry Pi from an NVMe SSD 

## From Pimoroni site 

### Firmware

Make sure your Raspberry Pi 5 firmware is up to date with the 2023-12-06 or later version. Software update on the RPi OS should do this for you, but you can force it by running: 

```bash
sudo rpi-eeprom-update 
```

in the Terminal. This will also tell you which firmware is running. 

 
### PCIe 3 Mode

To enable experimental and not-officially-supported PCIe 3 mode, add the follow line to the [all] section at the end of your Raspberry Pi /boot/config.txt file like this:

```bash
[all]
dtparam=pciex1_gen=3
```

Save and reboot - your drive is ready to use!

Formatting the NVMe and booting from NVMe

If you want to boot from the NVMe drive, follow these extra steps:

Make sure your firmware is updated as above
Format the drive using Raspberry Pi Imager
You can do this with your NVMe Base installed by booting the RPi 5 from SD card and running Raspberry Pi Imager from the start menu.
Open a Terminal.
Run sudo raspi-config 
Choose NVMe boot from the 'Advanced' section.
Reboot your RPi 5.


## From Jeff Gerling site 

### Power 

The NVMe hat uses around 5W of power but worth monitoring so that 

### Set NVMe early in the boot order

The PCIe connection should work after a reboot, but your Pi won't try booting off an NVMe SSD yet (at least, if there are any other boot devices present!). For that, you need to change the BOOT_ORDER in the Raspberry Pi's bootloader configuration:

Edit the EEPROM on the Raspberry Pi 5.

```bash
sudo rpi-eeprom-config --edit
```

Change the BOOT_ORDER line to the following:
```bash 
BOOT_ORDER=0xf416
```
Add the following line if using a non-HAT+ adapter:
```bash 
PCIE_PROBE=1
```
Press Ctrl-O, then enter, to write the change to the file.
Press Ctrl-X to exit nano (the editor).



## From Explaining Computers YouTube Channel 

### Set-up

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

### Speed Testing 

We can test the speed of the drive using the name of the ssd drive from the lsblk command: 

```bash 
sudo hdparm -t --direct /dev/nvme0n1
```

### How to boot from the NVMe SSD 

First of all fully update the pi and 

```bash
sudo apt update 
sudo apt upgrade 
sudo reboot 
```

We can edit the Eeprom configuration files with: 

```bash 
sudo rpi-eeprom-config --edit
```

We change the boot order to end with a 6 which corresponds to NVMe SSD if one is present: 

```bash
BOOT_ORDER=0xf416
PCIE_PROBE=1
```

The configuration PCI_PROBE=1 allows to enumerate over our PCIe bus. 