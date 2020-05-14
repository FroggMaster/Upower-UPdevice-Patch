# Upower UPdevice.c Patch

Upower patch to disable the lower power notification for wireless mice.

## Installation

Check your current Upower Version
```Bash
upower --version
```

Install dependencies

```Bash
sudo apt install gtk-doc-tools gobject-introspection libgudev-1.0-dev libusb-1.0-0-dev autoconf libtool autopoint
```
Download and patch UPowerd

```bash
git clone https://gitlab.freedesktop.org/upower/upower  
cd upower/src  
wget https://raw.githubusercontent.com/FroggMaster/Upower-UPdevice-Patch/master/updevice.patch
patch < up-device.patch  
cd ..  
./autogen.sh
./configure
make
```
Install Upowerd
```Bash
pushd .  
cd src/.libs  
strip upowerd  
sudo chown root.root upowerd  
sudo mv upowerd /usr/lib/upower/upowerd-silent  
cd /usr/lib/upower  
sudo mv upowerd upowerd-original  
sudo ln -s upowerd-silent upowerd  
popd
```
Install Upower
```Bash
pushd .  
cd tools/.libs  
strip upower  
sudo chown root.root upower  
sudo mv upower /usr/bin/upower-silent  
cd /usr/bin  
sudo mv upower upower-original  
sudo ln -s upower-silent upower  
popd
```

Restart Upower
```Bash
sudo systemctl restart upower
```

Check your Upower Version
```Bash
upower --version
```
