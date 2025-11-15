Goal: One might seek to get as many users to register on one private Meshcore channel by making that channel publically known, in order to have a platform where users might be able to submit ideas to the following challenge: "How might everyone be on the way to Pro?"  
  
Challenge: Once a private channel might go public, malicious users might be able to attack that channel, which might be inevitable. In order to prevent that from happening, there might need to be a mechanism by how to defend against such attacks.

Requirements:

Solution workflow:
Parts:
1. Client terminal: Wifi + Brower capable client device (Functionality: Select server Input text, read reply (with a one time pin code, and if the user types in the pin code, the cocktail might be served))
2. meshcore-Gateway: Wifi-AP + DHCP router + mDNS + server running web ui for client device + meshcore node sending encrypted and then fragmented payload (serves the local website to the client terminal, then forwards 
3. meshcore-loadbalancer: multiple meshcore nodes to send and receive encrypted and fragmented payload and check whether the sender-node might already blacklisted queue it for the RAG endpoint. It might 
4. RAG server: simple http server with a RAG system on a copy of 
