# Setup bridge mode in virt-manager

## Create a new bridge and change its state to up

```bash
ip link add name br0 type bridge
ip link set dev br0 up
```

## To add an interface (e.g. eth0) into the bridge, its state must be up

```bash
ip link set eth0 up
```

## Adding the interface into the bridge is done by setting its master to br0

```bash
ip link set eth0 master br0
```

## To show the existing bridges and associated interfaces, use the bridge utility

```bash
bridge link
```

## This is how to remove an interface from a bridge

```bash
ip link set eth0 nomaster
```

## The interface will still be up, so you may also want to bring it down

```bash
ip link set eth0 down
```

## To delete a bridge issue the following command

```bash
ip link delete br0 type bridge
```

## This will automatically remove all interfaces from the bridge. The slave interfaces will still be up, though, so you may also want to bring them down after
