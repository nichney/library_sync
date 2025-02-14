# Library Sync Script

This is a simple script for automatically synchronizing a local and remote directory.

## Configuration  
Configuration is stored in the file `/etc/lib_sync.conf`, which must contain:  

- **IP address** of the external server  
- **Username** on the external server  
- **Path to the directory**  
Example:
ip=192.168.1.100
user=myuser
libPath=/home/myuser/library

## Installation  

1. Copy the script to `/usr/bin/` for correct Systemd operation:  
   ```bash
   sudo cp library_sync /usr/bin/
   sudo chmod +x /usr/bin/library_sync
   ```

2. Copy systemd unit files to the user systemd directory:
   ```bash
   mkdir -p ~/.config/systemd/user/
   cp library_sync.service library_sync.timer ~/.config/systemd/user/
   ```

3. Reload systemd and enable the timer:
   ```bash
   systemctl --user daemon-reload
   systemctl --user enable --now library_sync.timer
   ```

## Usage
The script will run automatically based on the systemd timer settings. To check the status:

       systemctl --user list-timers --all | grep library_sync 

To view logs:

       journalctl --user -u library_sync.service --since "10 minutes ago"

To disable the sync timer:

       systemctl --user disable --now library_sync.timer


