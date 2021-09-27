## Create swap file

You may need to create a swap file in order to avoid the system from locking up during the build process.
On S922X you will need a total of 6GB of memory, meaning a 2GB swap if your device has 4GB of RAM and 4GB swap if it has 2GB of RAM.  
On S905* devices, you will need 4GB of memory, meaning no swap is necessary if your device has 4GB of RAM and 2GB swap is required if it has 2GB of RAM.  
Run the following commands to create and activate a 2GB swap file. Change the `count` value to adjust the swap file size.

```sh
dd if=/dev/zero of=/storage/.swapfile bs=1M count=2000
chmod 600 /storage/.swapfile
mkswap /storage/.swapfile
swapon /storage/.swapfile
```

You can place the following code in `/storage/.config/autosart.sh` to make the swap file persist across reboots.

```sh
#!/bin/bash

if [ ! -f /storage/.swapfile ]; then
    dd if=/dev/zero of=/storage/.swapfile bs=1M count=2000
    chmod 600 /storage/.swapfile
fi
mkswap /storage/.swapfile
swapon /storage/.swapfile
```
