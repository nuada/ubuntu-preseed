# Ubuntu preseed

## Netboot ISO
```
http://pl.mirror.archive.ubuntu.com/ubuntu/dists/trusty/main/installer-amd64/current/images/netboot/mini.iso
```

## Boot opions

Kernel boot options if DHCP is available:
```
auto=true url=<preseed URL>
```

To set specific IP for installed system use ``netcfg/get_ipaddress``:
```
auto=true url=<preseed URL> netcfg/get_ipaddress=<your IP>
```

To debug append ``DEBCONF_DEBUG=5`` to kernel command line.

## Serving preseed file

Minimal HTTP server using Python 2.x:
```
python -m SimpleHTTPServer 8000
```

## Preseed file

Create suitable preseed file by combining templates:
```
./seed minimal.template net-dhcp.template local-proxy.template partitions-boot-root-swap.template > seed
# or
./seed minimal.template net-static.template partitions-boot-crypto.template > seed
```
