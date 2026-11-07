#create ssh key pair 
	        > ssh-keygen -t ed25519   # the keys will be in ~/.ssh
# need to place the public key in remote server ---> .ssh/authorized_keys (the permission 600)
# the user must be existed on the remote server  IF local user name match the remote don't have to mention user in ssh command 
	        > ssh-copy-id user@ip_addres_remote_server # (will be asked for password of user on the remote server) 
      * there is also known_hosts file created on local key and it identify the remote machine,
     we can say it's the oposite of authorized_keys on remote server that identifie the local machine
# TO add password key on existed ssh key in this case : id_ed25519
	        > ssh-keygen -p -f .ssh/id_ed25519 
# when password added every ssh connection to server prompt to enter the password in this case we use ssh agent that keep the key in memory
            > eval 'ssh-agent -s' # this will initiate PID agent in  variable envirenoment check with
            > env | grep -i ssh_a
            > ssh-add  # without specify the key all the key will be loaded in agent  to check which one loaded and used
            > ssh-add -L  # once finish must kill the agent pid to avoid abuse it with
            > eval 'ssh-agent -k'
# use ssh to forward to another machine : there are 3 machines local -> jumpbox -> private the secure flow :
            > eval 'ssh-agent'  # on local machine
            > ssh-add
            > ssh -A user@jumpbox # the -A mean ssh with forwarding enabled 
      now on jumpbox
            > ssh user@private # on jumpbox
  OR THE MOST SECURE METHOD WITHOUT agent 
            > ssh -J user@jumpbox user@private 
            
