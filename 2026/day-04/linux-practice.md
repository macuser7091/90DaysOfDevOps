# Linux Practice: Processes and Services
## Process commands
- `ps` : Shows a report of current processes.
- `top` : Display a real time view of running processes.
## Service commands 
- `systemctl status` : Shows service status.
- `systemctl list-units` : List units that systemd currently has in memory.
## Log commands 
- `journalctl -u <service>` : `journalctl -u ssh` Shows log of ssh service.
- `tail -n 50` : `tail -n 50 /var/log/auth.log` Print last 50 lines of log file.
## Mini troubleshooting steps
- Step 1: Check service status. If service inactive/fail go to second step.
- Step 2: Check log file.
- Step 3: Find error in logs.
- Step 4: Resolve error.
### Step 1: Checking service status using command `systemctl status ssh`
- Output
```
ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Thu 2026-01-15 09:53:53 UTC; 1 week 5 days ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 1228 (sshd)
      Tasks: 1 (limit: 1008)
     Memory: 9.2M (peak: 17.0M)
        CPU: 1min 13.384s
     CGroup: /system.slice/ssh.service
             └─1228 "sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand /usr/share/ec2-instance-connect/eic_run_authorized_keys %u %f -o AuthorizedKeysCommandUser ec2-instance-connect [listener] 0 of 10-100 startups"
```
### Step 2: Checking log file using command `tail -n 10 /var/log/auth.log`
- Output
```
2026-01-27T17:55:01.850109+00:00 ip-172-31-17-215 CRON[49702]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
2026-01-27T17:55:01.854459+00:00 ip-172-31-17-215 CRON[49702]: pam_unix(cron:session): session closed for user root
2026-01-27T18:05:01.865443+00:00 ip-172-31-17-215 CRON[49730]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
2026-01-27T18:05:01.872124+00:00 ip-172-31-17-215 CRON[49730]: pam_unix(cron:session): session closed for user root
2026-01-27T18:12:06.120165+00:00 ip-172-31-17-215 sshd[49754]: Connection closed by 170.64.229.109 port 47068
2026-01-27T18:12:19.909563+00:00 ip-172-31-17-215 sshd[49755]: Connection closed by authenticating user root 170.64.229.109 port 37562 [preauth]
2026-01-27T18:15:01.878861+00:00 ip-172-31-17-215 CRON[49757]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
2026-01-27T18:15:01.885494+00:00 ip-172-31-17-215 CRON[49757]: pam_unix(cron:session): session closed for user root
2026-01-27T18:17:01.895281+00:00 ip-172-31-17-215 CRON[49767]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
2026-01-27T18:17:01.905501+00:00 ip-172-31-17-215 CRON[49767]: pam_unix(cron:session): session closed for user root 
```
### Everything looks good 
