![[Pasted image 20260818030912.png]]

When the service is making call outside of its scope and has no control over it i.e. database connection, another service. The service waits. The thread is responsible for waiting so that the service and later on complete the task. 

The whole java container have multiple thread that are reserved for handling request for the entrie app. By default, the call uses thread from those reserve. This causes a major issue during peak request for a service. Since, the thread that is being used by default is from the java container itself, high volume request on one service could end up maxing out all the java container thread and can crash the enitire java application. The bulkhead pattern is used so that the outliar thread could have their own thread pool so that even in the case of high traffic senerio where all its threads is maxed out, only the call to the service goes down not the entire application.

## Assigning threadpool size
![[Pasted image 20260818030813.png]]