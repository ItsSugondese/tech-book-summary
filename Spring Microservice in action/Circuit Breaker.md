In the case of a certain aspect of the program slowing down the process, the request to access the resource of that aspect causes the request to slow down. In small scale, the issue might not be visible but multiple aspects of the program directly or indirectly depends on that faulty aspect, it can leads to cascading effect and cause entire program to slow or shut down. 

![[Pasted image 20260706002639.png]]

For instance, in the above figure, lets suppose Network Access Storage (NAS) is where the fault exists. The cause for the fault being changes in the storage that causes the issue with read speed. Here, Application C is directly dependent with Service C so the issue is likely to occur in that application, but even Application A and B will in the long run might face issue even though the service they are dependent on is B but for some of the operations, they have to rely on Service C. 

When Service C starts running slowly, the thread pool of request starts backing up to complete the request. Not only that, In the case of transactional database request (Data Source A/B), it can exhaust  database connection pool since the whole transaction depends on Service C too to complete and the next request to the data source is halted till the whole transaction gets completed. Finally, Service A starts running out of resources because it’s calling Service B, which is running slow because of Service C. Eventually, all three applications stop responding because they run out of resources while waiting for requests to complete.

## Circuit Breaker

![[Pasted image 20260706004805.png]]Circuit breaker can avoids this scenario. It monitors the failures or timeout of the service and avoids new request to redirect to that service once certain threshold request is reached. The breaker can either make sure to throw exception or can be configured to redirect  request to fallback database/service temporarily to make sure the transaction gets completed.