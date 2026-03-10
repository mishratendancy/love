## Love

This project is an AI-assisted coding workflow built on **Spring Boot** with a **Spring Cloud API Gateway**, **LLM APIs with tools**, and a **RAG (Retrieval-Augmented Generation)** layer to avoid resending all code on every request and to reduce cost.

### High-level architecture (from the diagram)

- **User**: sends a prompt.
- **Spring Cloud API Gateway**: entry point for all requests from the user.
  - Forwards prompts to the thinking services.
  - Buffers content and stores it in a model store (for example, S3).
  - Sends the same data into the RAG system.
- **All the services (thinking part)**: backend services that orchestrate reasoning and call tools.
- **LLM APIs (has tools)**: large language model endpoints that can use tools to work with code, workspace, etc.
- **Workspace Service**: manages the user’s workspace, files, and code context.
- **Chat Service**: manages the chat session between the user and the AI.
- **All the session storage**: persists session state across interactions.
- **RAG**:
  - Stores relevant code and context chunks.
  - **Helps to not send all the code again and again**, reducing tokens and cost while keeping answers grounded.

### Request flow

1. **User prompt**
   - The user sends a prompt.

2. **Gateway routing**
   - The prompt goes through the **Spring Cloud API Gateway**.
   - The gateway buffers the content and writes it to storage (for example, an S3 bucket) and to the **RAG** index.

3. **Thinking services**
   - The gateway forwards the request to **thinking services**, which:
     - Pull context from **RAG**, session storage, and workspace.
     - Call **LLM APIs with tools** to perform reasoning and code operations.

4. **Workspace / chat services**
   - **Workspace Service** handles file and workspace operations.
   - **Chat Service** handles conversation state and formatting of the response.

5. **Response**
   - A response is generated and returned to the user through the **API Gateway**.

### Project initialization

I am cloning a project from **Lovable.dev** with **Spring Boot** as the backend, so I started with:

1. **Clone from Lovable.dev**

   ```bash
   git clone <lovable-dev-git-url>
   cd love
   ```

2. **Make sure Java is installed**

   - Install **JDK 17+**.
   - Verify:

     ```bash
     java -version
     ```

3. **Build the Spring Boot backend**

   - If it’s a Maven project:

     ```bash
     ./mvnw clean install
     ```

   - If it’s a Gradle project:

     ```bash
     ./gradlew build
     ```

4. **Run the app**

   - Maven:

     ```bash
     ./mvnw spring-boot:run
     ```

   - Gradle:

     ```bash
     ./gradlew bootRun
     ```

   - Or run the built jar:

     ```bash
     java -jar target/*.jar
     ```

### Notes

- RAG is used so we don’t have to resend all the code on each request, which helps with latency and cost.
- As the system evolves, update this README with concrete service names, storage details (e.g. exact S3 buckets), and deployment steps.

### Being “proper” (production-minded)

- **Clear contracts between services**: each service (gateway, thinking services, workspace, chat) should expose well-defined REST/gRPC APIs with versioning, so changes don’t break clients.
- **Observability**: add logging, metrics, and tracing across the gateway, thinking services, and LLM calls to debug issues and understand latency/cost.
- **Security**:
  - Protect the gateway with authentication/authorization (e.g. OAuth2/JWT).
  - Never log raw secrets or full prompts that may contain sensitive code.
  - Restrict access to storage (S3, RAG index, session store) with least-privilege policies.
- **Reliability**:
  - Use timeouts, retries, and circuit breakers on calls to LLM APIs and other services.
  - Add health checks and readiness/liveness probes for all Spring Boot services.
- **Cost-awareness**:
  - Prefer RAG lookups plus smaller prompts instead of sending the entire codebase.
  - Cache frequently used context and avoid unnecessary LLM calls in background jobs.


