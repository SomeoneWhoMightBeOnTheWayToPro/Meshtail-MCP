Goal: CNP (channel negotiation protocol) might seek to enable the negotiation of a new private one to one channel, in order to get as many users to register on one private Meshcore channel as possible without making that channel publically known, in order to have a platform where users might be able to submit ideas to the following challenge: "How might everyone be on the way to Pro?"  
  
Why might one need CNP?:  
One might understand one reason, why one might not seek to make such a channel publically avaiable through the following explaination: The specification for LoRaWAN (Long Range Wide Area Networks) might not be able to prevent DDoS (Distributed Denial of Service) attacks might be able to spam such private channel if publically given access to to the degree of unusuability. In times where one might be able to contact another through other methods this might not be a challenge. But in times where one might become dependent on such channel, one might become very vulnable to such attacks. One might appreciate the idea not to share access to such private channel carelessly. Even with utmost care, there might be furhter possible attacks, such as someone-in-the-middle attack, where someone might mimic a transit point to gain access to the content.  In order to prevent such attacks, specification of LoRaWAN requires encrpytion of messages. But even wit such encrpytion of messages, there might be spies who might be able to decrypt such messages. Threfore one might seek to further repeatedly decrypt such messages with asymmetric encryption in order to negotiate a new private channel where one might have one to one connection. That part of the project might be able to be referered as CNP, which might be a plain text based modified version of the TCP handshake.  
  
Specificaiton of CNP:  
1. Client might join the private broadcast channel with at least one administrator node.
2. Client generates a asymmetric encryption key which is different from the public meshcore key for encrpyting the messages within the private channel.  
3. "REQ + shortend meshcore public key" -> New client requests public key of the administrator node.  
4. Within a predefined time window, only the one current administrator node should answer. If other presuming administrator node might answer, this private channel might be declared as corrupt and a new channel might need to be instanciated. If the current administrator node might not answer, the first backup administrator node sends a "REQ + shortened meshcore public key" to ensure that the previous administrator node did not answer. After the timeout the first backup administrator node might reply with it's full public key as a plain text public key of the current administrator node. The client remembers both, the public meshcore key of the administrator node and the public message encryption key of the administrator node.  
5. Using that public key of the administrator node, the client encrypts its public encryption key which might be different from the public meshcore key, in order to protect oneself from other silent nodes eavesdropping on such a private channel. Once the administrator node has successfully received such a public message encryption key, the administrator node might create a new private channel, and it might send the credentials of that new private channel encrypted by such a public message encrption key of the client to the client. From this point on, the client might not reply in the private broadcast channel, except when a client node might send "BAN", the first backup administrator node might have to check the integrity of the current administrator node.   
6. Client joins the new private channel.
7. Once the client might have successfully decrypted such ACK message, the client might send a service request code to the administrator node which might be a hash, which the administrator node might have to know, otherwise it might send the following message and starts as fresh but remembers the public meshcore public key, in order to repeatedly try to guess service numbers: "RST" (Reset connection)  
Once multiple RST might be sent, the administrator node black lists such client node and might send a message in order to mark such node as banned to other administrator nodes, in order to prevent being marked offline: "BAN"  
There might be no way to redeem as a banned node as in: "One might seek not to negotiate with terrorists."  
8. Once the administrator node might recognize and then acknowledge the service request code with "ACK", the client might send or receive payload.  
9. Once the client might be satisfied with the request, it might send the message "FIN" and the administrator node might send "ACK", otherwise the client might repeated one more time sending "FIN". If the administrator node might not reply, the client might declare the request to be completed.
10. Client node might periodically change the encryption key, and when ever it might change its's key, it might send its new public encryption key encrpyted with the public encryption key of the administrator node. When the administrator node might change it's public key, client receives "BAN" in the one on one channel and the process might have to start anew. 
11. End.

Specification on how to implement CNP-application:
Parts:
1. CNP-Client:  
1.1 meshcore-Gateway : Wifi-AP + DHCP router + mDNS + server running web ui for client device + meshcore node sending encrypted and then fragmented payload (serves the local website to the client terminal, then forwards.  
1.2 Client terminal: Wifi + Brower capable client device (Functionality: Select server Input text, read reply (with a one time pin code, and if the user types in the pin code, the cocktail might be served)).  
  
2. CNP-Admnistrator node:
meshcore-load balancer: multiple meshcore nodes to send and receive encrypted and fragmented payload. Stores the connection of the two public keys (meshcore and message)

________________
The actual project:
service serve
1. Pin code server: and check whether the sender-node might already blacklisted queue it for the RAG endpoint. It might have a seperate channel where it exhanges blacklisted meshcore-nodes. If the suggestion by the client terminal was accepted by the RAG server, it might generate a PIN code as an answer. And that answer might be sent back to the gateway, where it might displayed at the appropriate client terminal. The PIN code might also be sent to the cocktail robot, where the user might be able to type in the PIN code in order to claim the liquid reward.
2. RAG server: simple http server with a RAG system on a copy of a document called "42" and evaluates, whether the suggested idea might be aligend with the document.
3. Cocktail Robot: Might get the PIN code from the meshcore-gateway and if it might be redeemed, it might mark that pin as redeemed.
