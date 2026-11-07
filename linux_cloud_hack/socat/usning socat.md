# usning socat
  # a simple  tcp connection send and receive and display data on the terminal on both  sides because of the flag -, also port should be open and listen in this case 8080 so the firewall is involved 
    > socat -  tcp4:10.0.0.198:8080     # this in machine 1 the sender 
    > socat  tcp4-listen:8080,fork,reuseaddr -         #   on the listener ,plus fork flag mean listen for multiple machine without it it accept only from one machine 
    #to send folders
    > tar cf - black_hat_bash | socat - TCP:10.0.0.198:8080  # put on one folder using tar 
    > tar czf - black_hat_bash | socat - TCP:10.0.0.198:8080  # to compress 


    
# exposing services :  we have python http server running on machine2(10.0.0.198) on local host so the web server will be not accessible form LAN (machine1 10.0.0.55) so we need om machine2  socat application listen on public interface and forward traffic to local host 
        > socat -v tcp4-listen:8080,fork,reuseaddr,bind=10.0.0.198 tcp4:127.0.0.1:8080  # on machine 2 
        > curl 10.0.0.198:8080   # on machine 1 
 
    
