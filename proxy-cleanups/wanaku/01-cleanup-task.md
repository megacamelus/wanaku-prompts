The taks is to refactor the code to decouple the Tool interface from the ToolsProxy.

The code should be simplified for maximum elegance, but still being extensible (for instance, the code for provisioning operation is mostly duplicated between the two). I would like you to consider that the role of the classes named Proxy, is to hide the complexities of the grpc invocation. In the future I may have more grpc services and I am looking for ways to refactor the code in such a way that adding new services doesn't fill cumbersome or overcomplex.
