
# Host Environment Construction Guide

* Install build tools

```bash
sudo pacman -S archiso
```

* Modify the configuration file

  * If you plan to use the KVM virtual machine as the host, no modification is required.
  * If you plan to use a virtual machine such as VirtualBox as a host, modify the value of the "harddrives" key in user_configureation.json to /dev/sda, /dev/sdb, or /dev/sdc.

* Create a configuration file directory for the build process

```bash
mkdir -p ./archiso
cd ./archiso
cp -r /usr/share/archiso/configs/releng/* ./
```

* Overwrite the configuration file in the configuration file directory.

```bash
cd ./archiso
cp -r path/to/rkos-build/airootfs ./
cp path/to/rkos-build/packages.x86_64 ./

```

* Build host image

```bash
cd ./archiso
mkarchiso -v -w work/ -o out/ ./
```

* Use kvm to run the built image to install the host system.

  * The configuration that needs to be confirmed is that three virtual disks must be configured. The first disk has a capacity of 20GB and is used for host system installation. The second disk is 30GB and is used as the target disk. The third disk is selected according to the actual situation. Block disk capacity plus memory capacity greater than 35GB
  * The installer will run automatically within about 5 minutes after the host image starts. After the installer starts, you need to manually select the install option, and you don’t need to set any options.
  * If it does not run automatically or runs incorrectly, execute the command manually: ```archinstall --config user_configuration.json --creds user_credentials.json --disk_layouts user_disk_layout.json```
  * After the installation is complete, you will be prompted whether to enter the chroot environment. Here,  you can choose no and then reboot.
  * After the host environment is installed, you need to manually mount the swap partition.
  * Host username root password root

* Automation script (Comming soon)

## References

[https://wiki.archlinux.org/title/archiso](https://wiki.archlinux.org/title/archiso)

[https://github.com/archlinux/archinstall](https://github.com/archlinux/archinstall)

[https://github.com/archlinux/archinstall/wiki/Building-and-Testing](https://github.com/archlinux/archinstall/wiki/Building-and-Testing)
