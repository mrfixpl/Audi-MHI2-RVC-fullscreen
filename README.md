# Audi MHI2 RVC fullscreen (Audi-MHI2-RVC-fullscreen)
Audi MIB2 MMI (MHI2) rear-view camera modification for fullscreen stream display

## TL;DR
Modify `displaymanager.json` params and update GUI assets to change the camera view.

### Most important commands
* `ssh root@10.173.189.1` - connect with MIB2 at 10.173.189.1 IP address (WLAN hotspot)
* `ssh root@x.x.x.x` - connect with MIB2 at x.x.x.x IP address (D-Link Ethernet-to-USB adapter)
* `mount -uw /net/mmx/mnt/app && mount -uw /net/mmx/mnt/system` - enable write filesystem
* `mount -ur /net/mmx/mnt/app && mount -ur /net/mmx/mnt/system` - go back to read-only filesystem
* `exit` - log out from MIB

## How to backup?
Create backups before doing anything else. You can select on of the following methods or us both (better safe than sorry, right?)

### SSH methon with local storage on unit
* `ssh root@10.173.189.1` - connect with MIB2 at 10.173.189.1 IP address (WLAN hotspot)
* `cd /etc/eso/production/` - go to production directory
* `cp displaymanager.json displaymanager.json.backup` create backup file of the displaymanager config
* `cd /eso/hmi/lsd/` - go to assets directory
* `cp -r images images_backup` - backup the GUI assets directory
* `exit`

### SCP method with download to your machine
* `mkdir ~/Downloads/MHI2_backups/production/`
* `mkdir ~/Downloads/MHI2_backups/images/`
* `scp root@10.173.189.1:/mnt/system/etc/eso/production/*.json ~/Downloads/MHI2_backups/production/`
* `scp -r root@10.173.189.1:/mnt/system/eso/hmi/lsd/images ~/Downloads/MHI2_backups/images`

## Procedure
* download assets from this repository
* upload selected assets to Audi MIB2 MMI unit
* reboot the unit
* check if it works and enjoy!

## Root passwords
* `4SapmKoq` - 

## Automatic write enabling on SSH connection
* `ssh root@10.173.189.1`
* `mount -uw /net/mmx/mnt/app`
* `echo "/bin/mount -uw /net/mmx/fs/sda0 2>/dev/null" >> /net/mmx/mnt/app/root/.profile`
* `echo "/bin/mount -uw /net/mmx/fs/sda1 2>/dev/null" >> /net/mmx/mnt/app/root/.profile`
* `echo "/bin/mount -uw /mnt/app" >> /net/mmx/mnt/app/root/.profile`
* `echo "/bin/mount -uw /mnt/system" >> /net/mmx/mnt/app/root/.profile`
* `mount -ur /net/mmx/mnt/app`
* `exit`
