![[Pasted image 20260614223941.png]]

Firstly, the service consumers (i.e. the applications) makes a network request to access the service by making a request to load balancer using DNS of the load blancer along with the service it wants to access. Once the request reaches the load balancer, it searches the service in the routing table(or backend pool configuration). The routing table contains the list of available server hosting the service and redirect the request to the active one. The activeness of server is analyzed by doing health monitoring of the available server of the particular service. 

Mostly, the process is handle by primary load balancer. But, as a safety-net, secondary load balancer is also kept in the case primary balancer goes down. It pings the primary LB for health monitoring and takes over in the case of failure. The routing table in most of the cases is replicated in secondary load balancer by making sure it sync with primary LB.

The server hosting the service has static configuration i.e. no wonder how many times the server is restarted, the IP address and other config will be same (intentionally) as it was before until and unless the configuration is changed manually. This approach is good for in-house server since the vertical scaling is pre-planned and manual changes is persistent. But,  its waste of potential when talking about cloud based microservice because scaling in cloud easy and scaling can be done based on the requirement i.e. up when traffic is high and down when its low. Since, this approach rely on manual config of hardware, the scaling up and down approach is achievable but is head-ache to setup.

![[Pasted image 20260615013726.png]]
