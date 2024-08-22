IP Spoofing :

IP spoofing refers to the process of creating and sending an IP packet for a certain destination using a different src address, then the actual source IP address.
Spoofing the source IP address can be possibly used for,
1. the purpose of concealing the identity of the sender or
2. impersonating another computing system (misleading the destination)
3. defeating network security measures, such as authentication based on IP addresses

Implemented attacks(mostly on Internet Protocol):

1. Denial Of Service attack (DOS attack)
   Goal          : To flood the victim with overwhelming amounts of traffic, without considering the responses to the attack packets.
   Prerequisites : No service/response is expected from the targeted machine, thus it makes up to the most basic form of attack.
   Strategy      : Saturating the target machine with external communications requests, such that it cannot respond to legitimate traffic, or 		   	           responds so slowly as to be rendered essentially unavailable (Server overload).
   Consequence   : Makes the network resource unavailable to its intended users.
                   Forces the targeted computer(s) to reset, or consume its resources so that it can no longer provide its intended service 		 	                Obstructing the communication media between the intended users and the victim so that they can no longer communicate adequately
                   
   - Implemented ICMP Flooding, 
     Source code : dos_attack.py
                 ICMP pacekts contained in IP packets are forwarded to the target, by using many different IP addresses along many threads           	              simultaneously, and each thread sends the IP packets indefinitely
	 Test command : sudo python dos_attack.py "target_IP_address"
	 Note : "impacket" module needed beforehand

2. ARP Poisoning
   ARP Introduction : ARP or Address Resolution Protocol defines the mapping from "network" layer [MAC layer] to the "link" layer [IP/TCP layer] 
   Each system on a network maintains its own ARP table, which keeps on updating at regular intervals of time
   Continuos updates to the ARP table are done by making use of the information catered from the received packets from all the nodes communicating    	 to this machine.
   Thus ARP poisioning can be readily implemented by sending a deceived ethernet packet containg the ARP packet, which misguides the destination      	 system about the MAC address of the source it assumes the packet has been received from.

   Goal          : To modify the ARP table of the targeted machine.
   Prerequisites : No support is expected from the targeted machine for the poisioning, but it does require the IP addresses of both the machine
                   being poisoned as well as the IP address of the corresponding entry of the ARP table.
   Strategy      : The ARP packet can either be sent directly to the targeted machine or be broadcasted(broadcasting is more preffered or else the 
                   differences in the IP-MAC mapping of the systems in a network results in poisoning being caught).
   Consequence   : All the packets routed towards the victim by the target are caught by IP spoofing system(because of the MAC address)
                   Any personal communications without private key encryption techniques can be easily tracked of, thus destroying the privacy
                   Man in the middle attack is the greatest threat on security that follows

                   
   - Implemented ARP poisioning, 
     Source code : arp_poisoning.py
                 ARP packets constructed through socket module only, are contained in the ethernet packet, and sent to the destination/broadcasted
                 ARP header contains our MAC address, target IP and victims IP.
				 MAC address need not be typed in by the spoofer, as it is automatically picked up by using some functions of "netifaces"
			     "netifaces" module is implemented, but is not mandatory
	 Test command : sudo python arp_poisoning.py "victim_ip" "target_ip"
	 Note : "netifaces" module needed beforehand

3. Spam ping
   Ping is sending of ICMP messages to a ping server and expecting back a reply from it. Sping also reffered as "trackback spam" denotes the pings
   sent from spam blogs, or multiple pings in a short interval from a source, to make the content coming from the source appesr fresh.

   Goal          : To send multiple pings, at a rate of around 100pings per minute
   Prerequisites : 
   Strategy      : Create an ICMP packet and send it with the spoofed
   IP address in the IP header. 
   Consequence   : Though it can be positively utilised to direct attention to recent blog posts, the service is being wrongly employed as a spamming techniques by different blogs to unnecessarily direct the readers to web pages that are not, in fact, recent blog posts 
                   
   - Implemented Spam ping, 
     Source code : sping.py
                 
	 Test command : sudo python sping.py <spoofed_ip> <destination_ip>


4. HTTP spoofing
   Spoofing is a situation in which a program successfully masquerades as another by falsifying data and thereby gaining an illegitimate.

   Goal          : Spoofing HTTP requests to a server by creating a
   TCP handshake session and then sending a simultaneous ack-get
   packet to successfully complete the handshake and receive a response.  
   Prerequisites : 
   Strategy      : Check the refferer header of the HTTP request, and then implementing the neccesary modifications
   Consequence   : Allows users to gain unauthorized access to the
   materials in situations where ip_address based authentication is used 
                   
   - Implemented HTTP spoofing, 
     Source code : http_spoofing.py
                 
	 Test command : sudo python spoofed_ip server_ip port
	 
