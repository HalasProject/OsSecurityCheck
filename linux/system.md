# System

## Limit access to `/boot/`🔴 

the **`/boot/`**folder contains our kernel so we should protect it

the file **`/boot/system.map`** contains the symbol tables used by the kernel associated with memory addresses ,This file is often the target of attacks aiming to exploit the flaws in the kernel code.

```text
ls -lrth / | grep boot
```

```text
dr-xr-xr-x. 5 root root 4,0K 27 mars 09:34 boot
```

![](../.gitbook/assets/system_map.png)

## Update 🔴 

Check the signature and effectiveness of the installer packages

```text
more /etc/apt/sources.list
```

List all packages installed in the system

```text
dpkg -l
yum list installed
```

Update system

```text
sudo apt-get update
sudo apt-get upgrade
```

