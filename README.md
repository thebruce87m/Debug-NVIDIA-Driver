# Debug-NVIDIA-Driver

Check your kernel

```bash
uname -r
```


Reinstall the DKMS (not the kernel)

```bash
sudo dkms remove nvidia/525.105.17 -k 5.15.0-70-generic
sudo dkms build nvidia/525.105.17 -k 5.15.0-70-generic
sudo dkms install nvidia/525.105.17
```


## Load the driver

```bash

# Find out info
modinfo nvidia

# Try to load it
sudo modprobe nvidia

# Check the status
nvidia-smi 
```

# Troubleshooting

Error:
```bash
sudo modprobe nvidia
modprobe: ERROR: could not insert 'nvidia': Exec format error
```

Check the output of:

```bash
sudo apt install --reinstall linux-headers-$(uname -r)
```

For me, I had some modules failing. I removed the failing modules, e.g.

```bash

# remove
sudo dkms remove systec_can/1.0.3 --all
sudo dkms remove evdi/5.2.14 --all

# Rerun, make sure no errors
sudo apt install --reinstall linux-headers-$(uname -r)

# Loaded this time!
sudo modprobe nvidia

# Status ok
nvidia-smi 
```


