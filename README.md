# r8125

dkms source for 2.5G/5G Ethernet LINUX driver r8125

![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/MONaH-Rasta/r8125?sort=semver&style=for-the-badge)

This repo provides lazy/easy way of having Realtek 2.5G/5G Ethernet LINUX r8125 driver in DKMS way so that you can keep this driver even after the kernel upgrade.

## Before use

This DKMS package is for Realtek RTL8125 / RTL8125B(G) (r8125 in module name) Ethernet, which is designed for the PCIe interface.

## Installation

The simplest way:

```bash
cd /tmp
wget -q https://github.com/MONaH-Rasta/r8125/releases/latest/download/r8125_amd64.deb
sudo dpkg -i r8125_amd64.deb
```

## Check current driver

```bash
lspci -k
```

Should be something like this:

```shell
...
04:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller (rev 05)
	Subsystem: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller
	Kernel driver in use: r8125
	Kernel modules: r8169, r8125
06:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8125 2.5GbE Controller (rev 05)
	Subsystem: ASUSTeK Computer Inc. RTL8125 2.5GbE Controller
	Kernel driver in use: r8125
	Kernel modules: r8169, r8125
07:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller (rev 02)
	Subsystem: Realtek Semiconductor Co., Ltd. RTL8111/8168/8411 PCI Express Gigabit Ethernet Controller
	Kernel driver in use: r8169
	Kernel modules: r8169
```

If kernel driver in use is still r8169 even after reboot, then use `r8125.conf` file to override.

```bash
sudo wget -q -O "/etc/modprobe.d/r8125.conf" https://github.com/MONaH-Rasta/r8125/blob/main/r8125.conf
sudo update-initramfs -u
sudo reboot
```

## Updating package

If you found this repo is outdated, just fork it, update with latest driver files from Realtek website and create release with new tag `v<version of new driver>`. Deb package will be compiled automaticaly and attach deb to release.

## LICENSE

GPL-2 on Realtek driver and the debian packaing.

## References

- [Realtek PCIe FE / GBE / 2.5G / 5G Ethernet Family Controller Software page](https://www.realtek.com/en/component/zoo/category/network-interface-controllers-10-100-1000m-gigabit-ethernet-pci-express-software)