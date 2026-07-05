# Service Discovery agent
Performs health check for all the microservice instance using the URL set for each instance during instance creation. After making the network call in that URL(by pinging), if the response it gets is error, it removes the instance from the routing table to ensure that the client doesn't interact with the failed instance and making the operation smooth. In addition, it can also decide whether to shut down the failed instance or bring additional instance up.

# Service Discovery Architecture
The architecture is has 4  major implementations:

- Service registration for discovery
- Client figuring out service address
- Different services sharing information among each others
- Performing health monitoring by [[#Service Discovery agent]]


![[Pasted image 20260618165713.png]]

When a service instance comes online, it [[#Service Instance Registration |registers]] itself with one discovery instances under a service ID. In the case of multiple discovery instance, service instance details is shared among other discovery instance using peer-peer model (which include service instance health information). The registered service can then be looked up in the service discovery agent using the registered name. In the case of service failure, it stops sending heartbeat and once the discovery instance stops receiving the heartbeat, it removes the registration details of that service instance and stops routing the request to that instance.

## Client POV
*Note: Here, the client is backed and is trying to communicate with another backed instance.*

Once the registration is completed, when client needs to access a service, it reaches out to discovery instance and the discovery instance sends the client list of healthy service instances and client makes their request directly on any of those instances.

![[Pasted image 20260618174249.png]]
The another approach for service discovery by a client is to use client-side load balancing which basically stores the copy of service instance as a cache from service discovery and make the request directly to service instances using the service IP. The request is made to discovery instance periodically and cache is updated in the case of any changes. If the request made using client load balancer is redirected to dead service instance, the load balancer makes request instantly to discovery instance and updates the service instances cache.
## Service Instance Registration
The service register registers itself in service discovery instance using DNS or combination of IP address and port number. By default, registration is done by DNS but in docker-containers, the default hostname is random generated value which results in confusing naming convention because of which in this case IP address is considered for registration because of ease of reading and also to reduce host search failure rate since its easy to lookup the services based on IP address (172.18.0.15:8080) than random string (like abc123def456:8080) .