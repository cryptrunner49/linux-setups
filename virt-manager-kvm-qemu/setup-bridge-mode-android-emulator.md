# Setup bridge mode on android emulator on linux

## QEMU WiFi Bridge Connection

### Create the bridge: First, create the bridge interface on the host system. This can be done using brctl or ip commands. For example

```bash
sudo ip link add br0 type bridge
```

### Add the Ethernet interface to the bridge: Add the Ethernet interface (e.g., eth0) to the bridge

```bash
sudo ip link set eth0 master br0
```

### Create a TAP device: Create a TAP device (e.g., tap0) for the WiFi interface

```bash
sudo ip tuntap add mode tap tap0
```

### Set the promiscuous mode on

```bash
sudo ip link set dev tap0 up promisc on
```

### Configure the Tap interface (e.g., tap0) to use the Bridge device

```bash
sudo ip link set tap0 master br0
```

## Start the emulator using the tap interface as argument

```bash
emulator -avd 'Pixel_7_API_32' -verbose -wifi-tap 'tap0'
```

## Delete the android wifi tap bridge

```bash
ip link set tap0 down
ip link set tap0 nomaster
ip link delete tap0
```
