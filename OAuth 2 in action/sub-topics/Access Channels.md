#Access_Channels
Two types of access channel exists both with their own use-cases. 
### Back Channel
Here, the communication between client and resource server happens without the needs for clients. For instances, taking photo from cloud and run jobs to generate library everyday.

The back channel happens in several ways. Mainly through the combination of access and refresh token. Access Token is used for getting the resource, and when it expires, the resource token having relatively higher expire time can be used to get new access token and get resources without users intervention.

### Front Channel
This is the important one and without this back channel is not possible. Basically, front channel is when the interaction happen with client and resource server indirectly mainly through the use of redirection. To be clear, users are ensure if they want to let client access resource server or not making it indirect i.e. through the user interaction mainly using web browser as a medium. 

Firstly, the client redirects the user to authorization server using redirect link and once user validates himself auth server, the auth server redirects the user back to client with required credentials that would be needed by client for further use. Once, validation completes,  [[#Back Channel]] happens between client and resource server.