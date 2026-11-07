# if one of those 2 command give : Status: inactive
    > ufw status numbered
    > ufw status verbose
# must use :     
    > ufw enable  # this will activate the rules already set so it's good to set the rules when the status is inactive,then enable 
    > ufw disable
    > ufw reset
#  
    > ufw allow ssh
    > ufw show added  # good one to know which rule been added 
    > ufw delete allow ssh
