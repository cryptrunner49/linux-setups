# Converting disks to qemu format

## Convert .vdi to .img format

```bash
vboxmanage clonemedium ubuntu-desktop-22.04.vdi ubuntu-desktop-22.04.img --format raw
```

## Convert .img to .qcow2

```bash
qemu-img convert -f raw ubuntu-desktop-22.04.img -O qcow2 ubuntu-desktop-22.04-new.qcow2

rm ubuntu-desktop-22.04.img
```

## Noop conversion (qcow2-to-qcow2) removes sparse space

```bash
qemu-img convert -O qcow2 source.qcow2 shrunk.qcow2
```

## You can also try add compression (-c) to the output image

```bash
qemu-img convert -c -O qcow2 source.qcow2 shrunk.qcow2
```
