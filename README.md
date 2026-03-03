## Love

I am cloning a project from **Lovable.dev** with **Spring Boot** as the backend, so let me start by setting up the basics.

### How I initialized the project

1. **Clone from Lovable.dev**

   ```bash
   git clone <lovable-dev-git-url>
   cd love
   ```

2. **Make sure Java is installed**

   - Install **JDK 17+** on your machine.
   - Confirm it works:

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

- I’ll add more details later about the Lovable.dev setup, frontend, and deployment.
- Update commands/paths above to match the exact structure once the project stabilizes.



