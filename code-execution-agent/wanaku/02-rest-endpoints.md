Create a REST API implementation for the Wanaku code-execution engine with the following specifications:

Implement REST endpoints under the new base path /api/v2/code-execution-engine with hierarchical routing structure /api/v2/code-execution-engine/${engine-type}/${language}.

Create two primary endpoints:

First endpoint: POST /api/v2/code-execution-engine/${engine-type}/${language} - accepts code submission, validates and accepts the code, generates a random UUID representing the code execution task, returns HTTP 201 Created with Location header or response body containing the auto-generated SSE stream endpoint URL in format http://host:8080/api/v2/code-execution-engine/${engine-type}/${language}/${task-uuid}.

Second endpoint: GET /api/v2/code-execution-engine/${engine-type}/${language}/${task-uuid} - serves as Server-Sent Events (SSE) endpoint that streams execution responses back to the caller for the specified task UUID.

Define all necessary data types, request/response models, and DTOs required for these endpoints including code submission payloads, task identifiers, SSE event structures, and error responses.

Implement proper HTTP status codes, headers for SSE streaming (Content-Type: text/event-stream, Cache-Control: no-cache, Connection: keep-alive), and RESTful conventions.

Do not implement business logic for code execution, validation, or stream processing - only create the endpoint definitions, routing infrastructure, data models, and controller/handler method signatures with placeholder implementations that acknowledge the request and return appropriate mock responses.
