# Day 05 assignment – Linux Troubleshooting Drill: CPU, Memory, and Logs
## Linux troubleshooting runbook
### Step 1: Capture a quick health snapshot
- OS & kernel (system identity) `uname -a`, `cat /etc/os-release`
- CPU / Memory pressure `top`, `htop` / `free -h`
- Disk / IO `df -h`, `du -sh /var/log` / `iostat`, `vmstat`, `dstat`
- Network `ss -tulpn`, `netstat -tulpn`, `ping`
### Step 2: Filesystem sanity check
- Create a temp folder `mkdir /tmp/runbook-demo`
- Copy a file `cp /etc/hosts /tmp/runbook-demo/hosts-copy && ls -l /tmp/runbook-demo`
- list folder 
  - Reason: Filesystem read/write working or mot
### Step 3: Check logs
- Check last 50 logs `journalctl -u <service> -n 50`, `tail -n 50 /var/log/...`

## Practice runbook
### Target service - Docker
### Step 1
#### System identity
- `uname -a` Checking system information
  - Output
  ```
  Linux ip-172-31-17-215 6.14.0-1018-aws #18~24.04.1-Ubuntu SMP Mon Nov 24 19:46:27 UTC 2025 x86_64 x86_64 x86_64 GNU/Linux
  ```
- `cat /etc/os-release` Checking detailed information about system
  - Output
  ```
  PRETTY_NAME="Ubuntu 24.04.3 LTS"
  NAME="Ubuntu"
  VERSION_ID="24.04"
  VERSION="24.04.3 LTS (Noble Numbat)"
  VERSION_CODENAME=noble
  ID=ubuntu
  ID_LIKE=debian
  HOME_URL="https://www.ubuntu.com/"
  SUPPORT_URL="https://help.ubuntu.com/"
  BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
  PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
  UBUNTU_CODENAME=noble
  LOGO=ubuntu-logo
  ```
#### Snapshot: CPU & Memory
- `htop` CPU usage 0~1% (No cpu usage)
- `free -h` Memory usage 24% (Everything looks normal)
  - Output
  ```
                 total        used        free      shared  buff/cache   available
  Mem:           914Mi       439Mi       198Mi       2.8Mi       447Mi       474Mi
  Swap:             0B          0B          0B
  ```
#### Snapshot: Disk & IO
- `df -h` Disk usage 61% (Looks normal)
  - Output
  ```
  Filesystem       Size  Used Avail Use% Mounted on
  /dev/root        6.8G  4.1G  2.7G  61% /
  tmpfs            458M     0  458M   0% /dev/shm
  tmpfs            183M  968K  182M   1% /run
  tmpfs            5.0M     0  5.0M   0% /run/lock
  efivarfs         128K  4.7K  119K   4% /sys/firmware/efi/efivars
  /dev/nvme0n1p16  881M  155M  665M  19% /boot
  /dev/nvme0n1p15  105M  6.2M   99M   6% /boot/efi
  tmpfs             92M   12K   92M   1% /run/user/1000
  ```
- `vmstat` Checking information about system processes, memory, paging, block I/O, and CPU activity.
  - Output
  ```
  procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
   r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
   2  0      0 203248  11240 447572    0    0     6    10   82    0  0  0 100  0  0  0
  ```
 #### Snapshot: Network
 - `ss -tulpn` Checking network
   - Output
   ```
   Netid              State               Recv-Q               Send-Q                                  Local Address:Port                              Peer Address:Port              Process              
    udp                UNCONN              0                    0                                           127.0.0.1:323                                    0.0.0.0:*                                      
    udp                UNCONN              0                    0                                          127.0.0.54:53                                     0.0.0.0:*                                      
    udp                UNCONN              0                    0                                       127.0.0.53%lo:53                                     0.0.0.0:*                                      
    udp                UNCONN              0                    0                                  172.31.17.215%ens5:68                                     0.0.0.0:*                                      
    udp                UNCONN              0                    0                                               [::1]:323                                       [::]:*                                      
    tcp                LISTEN              0                    4096                                       127.0.0.54:53                                     0.0.0.0:*                                      
    tcp                LISTEN              0                    511                                           0.0.0.0:80                                     0.0.0.0:*                                      
    tcp                LISTEN              0                    4096                                          0.0.0.0:22                                     0.0.0.0:*                                      
    tcp                LISTEN              0                    5                                             0.0.0.0:4330                                   0.0.0.0:*                                      
    tcp                LISTEN              0                    4096                                        127.0.0.1:42963                                  0.0.0.0:*                                      
    tcp                LISTEN              0                    5                                             0.0.0.0:44321                                  0.0.0.0:*                                      
    tcp                LISTEN              0                    4096                                    127.0.0.53%lo:53                                     0.0.0.0:*                                      
    tcp                LISTEN              0                    511                                              [::]:80                                        [::]:*                                      
    tcp                LISTEN              0                    4096                                             [::]:22                                        [::]:*                                      
    tcp                LISTEN              0                    5                                                [::]:4330                                      [::]:*                                      
    tcp                LISTEN              0                    5                                                [::]:44321                                     [::]:*                                 
    ```
- `netstat -tulpn` Checking network
  - Output
  ```
  (No info could be read for "-p": geteuid()=1000 but you should be root.)
  Active Internet connections (only servers)
  Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
  tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN      -                   
  tcp        0      0 0.0.0.0:80              0.0.0.0:*               LISTEN      -                   
  tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -                   
  tcp        0      0 0.0.0.0:4330            0.0.0.0:*               LISTEN      -                   
  tcp        0      0 127.0.0.1:42963         0.0.0.0:*               LISTEN      -                   
  tcp        0      0 0.0.0.0:44321           0.0.0.0:*               LISTEN      -                   
  tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN      -                   
  tcp6       0      0 :::80                   :::*                    LISTEN      -                   
  tcp6       0      0 :::22                   :::*                    LISTEN      -                   
  tcp6       0      0 :::4330                 :::*                    LISTEN      -                   
  tcp6       0      0 :::44321                :::*                    LISTEN      -                   
  udp        0      0 127.0.0.1:323           0.0.0.0:*                           -                   
  udp        0      0 127.0.0.54:53           0.0.0.0:*                           -                   
  udp        0      0 127.0.0.53:53           0.0.0.0:*                           -                   
  udp        0      0 172.31.17.215:68        0.0.0.0:*                           -                   
  udp6       0      0 ::1:323                 :::*                                -       
  ```
### Step 2: Filesystem sanity check
- Filesystem woorking perfectly
### Step 3: Checking logs and Finding error
- `journalctl -u docker -n 20` Checking logs
  - Output
  ```
  Jan 15 09:52:44 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:44.557132348Z" level=info msg="[graphdriver] using prior storage driver: overlay2"
  Jan 15 09:52:44 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:44.598179922Z" level=info msg="Loading containers: start."
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.028010058Z" level=warning msg="Error (Unable to complete atomic operation, key modified) deleting object [endpoint_count 5710d>
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.078477754Z" level=info msg="Loading containers: done."
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.110577459Z" level=info msg="Docker daemon" commit="28.2.2-0ubuntu1~24.04.1" containerd-snapshotter=false storage-driver=overla>
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.111196657Z" level=info msg="Initializing buildkit"
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.116908796Z" level=warning msg="CDI setup error /etc/cdi: failed to monitor for changes: no such file or directory"
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.116939783Z" level=warning msg="CDI setup error /var/run/cdi: failed to monitor for changes: no such file or directory"
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.137465339Z" level=info msg="Completed buildkit initialization"
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.149660450Z" level=info msg="Daemon has completed initialization"
  Jan 15 09:52:45 ip-172-31-17-215 dockerd[868]: time="2026-01-15T09:52:45.149734593Z" level=info msg="API listen on /run/docker.sock"
  Jan 15 09:52:45 ip-172-31-17-215 systemd[1]: Started docker.service - Docker Application Container Engine.
  Jan 29 10:55:18 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:55:18.019494135Z" level=warning msg="Failed to allocate and map port: failed to bind host port for 0.0.0.0:80:172.17.0.2:80/tcp: add>
  Jan 29 10:55:18 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:55:18.070834275Z" level=info msg="ignoring event" container=2fee8f3bae54def32956e9f5491a03c80ad517082f813be1bf3854b8092f25b3 module=>
  Jan 29 10:55:18 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:55:18.129436152Z" level=error msg="Handler for POST /v1.50/containers/2fee8f3bae54def32956e9f5491a03c80ad517082f813be1bf3854b8092f25>
  Jan 29 10:55:19 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:55:19.011094054Z" level=warning msg="MAC address changed" eid=21265200f87c0915fff829bd3613b626d81175e8bd3d76ebb4eff68c980b22b0 ep=el>
  Jan 29 10:58:10 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:58:10.330498753Z" level=info msg="ignoring event" container=f4aefaa571eda75bb8f87c8a067d3490523e4933fbec3365531ce3ddea3028cf module=>
  Jan 29 10:59:12 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:59:12.176544732Z" level=info msg="ignoring event" container=a4701b6d836a1271c5e5a8a62deeff46ebc25ca8d92c24802d896f98e1306ae0 module=>
  Jan 29 11:13:39 ip-172-31-17-215 dockerd[868]: time="2026-01-29T11:13:39.905267517Z" level=info msg="ignoring event" container=54f456bc82641e1608f37f9b6509a3c63e13c4c2e639f73db11b31dc01c3293d module=>
  Jan 29 11:14:28 ip-172-31-17-215 dockerd[868]: time="2026-01-29T11:14:28.067653938Z" level=info msg="ignoring event" container=f361a2dfeeeed53da56d6a152e9f0449d4bdc89125166fe9cd496e8a2795bb7c module=>
  ```
- `journalctl -u docker -n 20 | grep -i "level=error"` Finding error
  - Output
  ```
  Jan 29 10:55:18 ip-172-31-17-215 dockerd[868]: time="2026-01-29T10:55:18.129436152Z" level=error msg="Handler for POST /v1.50/containers/2fee8f3bae54def32956e9f5491a03c80ad517082f813be1bf3854b8092f25b3/start returned error: failed to set up container networking: driver failed programming external connectivity on endpoint elastic_yalow (21265200f87c0915fff829bd3613b626d81175e8bd3d76ebb4eff68c980b22b0): failed to bind host port for 0.0.0.0:80:172.17.0.2:80/tcp: address already in use"
  ```
### Next step
- Problem: Port no. 80 allready in use
- Solution: Use another port no. 8080
