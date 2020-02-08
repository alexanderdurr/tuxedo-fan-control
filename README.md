## Adapted Fan Control for a Tensorbook
A Tensorbook is basically a Clevo P95xER. You can make sure you have one with:
```
sudo dmidecode | grep 'Product Name'
```
This repo is a fork of the original tuxedo-fan-control.
The changes to the original are in

    tuxedo-fan-control/src/electron/electronmain.ts
where I changed line 24 to false,
and in

    tuxedo-fan-control/src/data/fantables.json
the the fantable was adjusted to an reasonalble one for machine learning tasks.
The original build and install from source was adjusted for the tensorbook with preinstalled lambda stack.

![Alt text](src/data/fantable.jpg?raw=true "Fan Table")

# TuxedoFanControl

# Induction
The TUXEDO Fan Control is a Application and Daemon for controlling the fans of CPU and GPU of your TUXEDO Notebook device.

User Manual: [user_manual.md](./docs/user/user_manual.md)   
Dev Manual: [dev_manual.md](./docs/dev/dev_manual.md)

## Development

### Dependencies
- Node.js (Version >=10)
- gcc
- NVIDIA SMI for Controlling the NVIDIA GPU Fan (Only need at devices with nvidia graphic cards)
- Xvfb (X Window Virtual Framebuffer)

### Build from source

1. Install NodeJS 10:

On Ubuntu, follow these instructions:

Install curl:

```sh
sudo apt install curl
```

The curl package is most likely installed by default. Then proceed to add the required repository and proceed:

```sh
sudo curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
```

Now, you may proceed with installing nodejs and build-essential packages:

```sh
sudo apt install nodejs autoconf automake build-essential gcc g++ make rpm
```


2. Clone the Repo:
```sh
git clone https://github.com/alexanderdurr/tuxedo-fan-control && cd tuxedo-fan-control
```

3. Install the Node dependencies
```sh
sudo npm install
```

4. Build the Project:
```sh
sudo npm run build
```

### Create Packages (deb, snap, AppImage, rpm, tar.gz)
```sh
sudo npm run build && sudo npm run pack
```

#### To install the derived packages:

You will find all artifacts under the `output/build` directory.
To install, for instance, on Ubuntu use `gdebi` provided by `gdebi-core` and run:

```sh
sudo apt install gdebi-core
sudo gdebi output/build/*.deb
```

In case you want to uninstall the whole thing, run
```sh
sudo apt-get purge tuxedofancontrol
```

### Useful files
Log files (e.g. for reading sensor data):
```sh
cd /var/log/tuxedo-fan/tuxedo-fan-daemon.log
```
Daemon service:
```sh
cd /etc/systemd/system/tuxedofancontrol.service
```
Useful to restart the daemon:
```sh
sudo systemctl restart tuxedofancontrol.service
```
To see if the daemon is running fine:
```sh
sudo systemctl status tuxedofancontrol.service
```
