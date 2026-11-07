# create miniserver as user 
# This is the correct command when you want to create a brand-new service from scratch.
    > systemctl edit --force --full --user miniserver  # without sudo
    
# paste 

 
[Unit]
Description=Miniserve File Server
After=network.target

[Service]
WorkingDirectory=/home/yasine/Downloads
ExecStart=/usr/local/bin/miniserve .           # adapted to bath check it with which command
Restart=always
RestartSec=3

[Install]
WantedBy=default.target
    
    
# new file added at : yasine@ubuntu:~$ cat  ~/.config/systemd/user/miniserver.service 

# run : yasine@ubuntu:~$ systemctl cat --user miniserver.service 

#        > loginctl show-user yasine   # very hopeful loginctl command (loging manager) it info about the user 
#        > sudo loginctl enable-linger yasine  # this enable the ( var : linger)  

# after saving the file reload
        > systemctl --user daemon-reexec
        > systemctl --user daemon-reload
# now for   IPAddressDeny/IPAddressAllow here is what's going 
  even with this instructions 
  > systemctl edit --user miniserver   # and past 
  
[Service]
IPAddressDeny=any
IPAddressAllow=10.0.0.36

the service still accessed  y the other host 
When IPAddressAllow/Deny is actually useful

Your systemd setting is still useful—but for a different purpose:

Prevent your service from calling external APIs
Lock it to internal services only
Reduce damage if the service is compromised

Think of it as outbound sandboxing, not access control.

# When you run miniserve manually, its output goes straight to your terminal (stdout/stderr). But when it’s run as a systemd --user service, that output is captured by the systemd journal instead of being printed on screen.
So your logs are still there—you just need to view them differently.
👉 Check logs with journalctl
Use:

        > journalctl --user -u miniserver

To follow logs live (like running it manually):
        > journalctl --user -u miniserver -f

To see only recent logs:

        > journalctl --user -u miniserver --since "10 minutes ago"

   
