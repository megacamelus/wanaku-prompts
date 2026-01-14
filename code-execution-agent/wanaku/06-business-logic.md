With all the activities in place (for details, check all the files within the code-execution-agent directory to understand the context accross different projects), it is time to implement the business logic.


When a code execution request is received via the REST API (i.e.: a POST to /api/v2/code-execution-engine/${engine-type}/${language}), the code needs to query the capabilities repository to search for code-execution-engine service that can handle the code of the provided engine-type (in this case it needs to search the DB for a serviceType "code-execution-engine", a serviceSubType matching the engine-type and a serviceName that matches with the language). 

Then, it needs to modify the bridge to do the communication. This includes: 

1. Adding the  the new command (which was generated as part of wanaku-capabilities-sdk/03-exchange.md)  in the gRPC transport 
2. Adding a new CodeExecution bridge to communicate with the service 
3. Then calling the bridge methods on the business layer
