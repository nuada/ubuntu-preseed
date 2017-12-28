# Ubuntu preseed templates

## ISO

* [Ubuntu 16.04 (xenial) mini ISO](http://pl.mirror.archive.ubuntu.com/ubuntu/dists/xenial/main/installer-amd64/current/images/netboot/mini.iso)
* [Ubuntu 16.04.3 (xenial) server ISO](http://pl.releases.ubuntu.com/16.04.3/ubuntu-16.04.3-server-amd64.iso)

## UEFI

Standard `mini.iso` does not support UEFI booting.

To make it UEFI bootable:
1. Format USB drive to FAT32 with GUID Partition Map
2. Copy contents of `mini.iso`
3. Copy `EFI` directory from `ubuntu-16.xx.y-server-amd64.iso`

## Boot options

Kernel boot for loading preseed file over HTTP:
```
auto=true url=<preseed URL>
```
If DHCP is not available Debian installer will request manual network configuration after attempting DHCP.

To debug append ``DEBCONF_DEBUG=5`` to kernel command line.

## Serving preseed file

Minimal HTTP server using Python 2.x:
```
python -m SimpleHTTPServer 8000
```

## Preseed file

Create suitable preseed file by combining templates, eg.:
```
./seed minimal.template net-dhcp.template local-proxy.template partitions-boot-root-swap.template > seed
```
or
```
./seed minimal.template net-static.template partitions-boot-crypto.template > seed
```
