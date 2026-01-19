The task is to implement a feature for this project that works like this: 

1. It receives a Camel Route, in written in the YAML DSL, via the gRPC bridge (i.e.: the service in the CodeExecutorService class)
2. Then, it loads the route in code into a Camel Context (see reference implementation WanakuRoutesLoader.java) 
3. Camel does not support loading routes from memory. This is not natively supported by Camel, as such you will need to implement a custom ResourceResolver and Resource (link to a sample implementation is provided below) 

References: 

WanakuRoutesLoader: https://github.com/wanaku-ai/camel-integration-capability/raw/refs/heads/main/src/main/java/ai/wanaku/capability/camel/util/WanakuRoutesLoader.java
Sample Resource class: https://raw.githubusercontent.com/apache/camel/refs/heads/main/components/camel-resourceresolver-github/src/main/java/org/apache/camel/github/GistResource.java
Sample ResourceLoader class: https://github.com/apache/camel/blob/main/components/camel-resourceresolver-github/src/main/java/org/apache/camel/github/GistResourceResolver.java




