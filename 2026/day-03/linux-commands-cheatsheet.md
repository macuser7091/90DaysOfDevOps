# Linux command cheat sheet
## Process management
- `ps` : Show current processes.
- `top` : Display system summary and list of prrocesses or threads currently managed by kernal.
- `htop` : It is similar to `top`, but allows scroll vertically and horizontally. you can observe all running processes along with their command line arguments.
- `pstree` (Adv) : Shows running processes as a tree.
- `kill` : `kill [PID}` Kill process.

## File system
### Navigation and Viewing
- `ls` : List directory content.
- `pwd` : Shows present working directory.
- `cd` : To change directory.
- `cat` : Print file content on display.
- `find` : Search file in a directory.
- `head` / `tail` : `head` Output the first part of file. `tail` Output the last part of the file.
### File and Directory Management
- `mkdir` : Make a directory.
- `touch` : Make a file.
- `rmdir` : Remove empty directories.
- `rm` : Remove files or directories.
- `rm -r` : Remove directory and their content recursively.
- `cp` : Copy file or directory.
- `mv` : Move / Rename file or directory.
- `ln` (Adv) : Make links between files.
### Disk Management and Permissions
- `df` : Shows space usage.
- `du` (Adv) : Shows estimate file space usage.
- `mount` : Mount a filesystem (storage).
- `chmod` : Change file permissions.
- `chown` : Change file owner and group.
## Networking troubleshooting
### Basic Connectivity and Reachability
- `ping` : Ping any website to check its working or not.
- `traceroute` : 
- `tracepath` (Adv) :
- `nc` (Adv) :
- `telnet` (Adv) :
### Network Interface Information
- `ip addr` : (Modern replacement of `ifconfig`) Displays IP addresses, interface status.
- `ip route` : (Modern replacement of `route`) Shows the kernel routing table, which determines how network packets are directed to their destinations.
### DNS and Port Analysis
- `nslookup` : 
- `netstat` : Displays detailed information about network sockets, including established connections, listening ports, and associated process IDs.
