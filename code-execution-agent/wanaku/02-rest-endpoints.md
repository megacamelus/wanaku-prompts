The project is adding a code-execution engine for Wanaku.

Your task is to create a set of rest endpoints for this project. 

These new endpoints use a new base address at /api/v2, as they represent a newer approach to the problem this project tries to solve. 

The base address for operations of these new rest endpoints is /api/v2/code-execution-engine, with a further separation by the type of the engine and the language (i.e.: /api/v2/code-execution-engine/${engine-type}/${language}). 

You also have to add the data types, but you should not create the business logic yet (it will be defined at a later moment).

With those considerations in mind, there should be the following new endpoints:

- one new endpoint where the code is posted. If the code is successfully accepted, the endpoints returns the address of the endpoint in which the code can consume the response stream (as in HTTP SSE). This address is auto-generated and contains a randomly generated UUID that represents the code execution task (i.e: http://host:8080/api/v2/code-execution-engine/${engine-type}/${language}/${task-uuid})
- one new endpoint where the responses are streamed back to the caller (i.e.: http://host:8080/api/v2/code-execution-engine/${engine-type}/${language}/${task-uuid})
