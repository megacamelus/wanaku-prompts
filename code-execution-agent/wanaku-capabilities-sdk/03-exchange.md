The project is adding a code-execution engine for Wanaku. This project is the core framework used by Wanaku and its capabilities.

Your task is to create the protobuf message specifications for the communication between the microservices that use this framework.

In the capabilities-exchange module, you can find the existing message specifications for this project. The newly created specifications should respect the standards and norms used on those. 

As part of the communication in this project, these components now have to exchange the following data: 

Direction client to server: 
- A text blob, containing code to be executed by the service
- An optional map of string keys and string values, containing the arguments to the code execution 

As a response for this call, the server streams the execution of the code to the client, closing the gRPC channel upon completion.
