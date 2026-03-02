## Love

This project is being created by **cloning a Lovable.dev project** and using **Spring Boot** as the backend.

### Project initialization

I am starting this project by:

1. **Cloning from Lovable.dev**

   - Go to your Lovable.dev project page.
   - Copy the Git URL that Lovable.dev provides.
   - Clone it locally:

     ```bash
     git clone <lovable-dev-git-url>
     cd love
     ```

2. **Setting up Spring Boot backend**

   - Ensure you have a **JDK (Java 17+ recommended)** installed.
   - If using Maven:

     ```bash
     ./mvnw clean install
     ```

   - If using Gradle:

     ```bash
     ./gradlew build
     ```

3. **Running the Spring Boot application**

   - With Maven:

     ```bash
     ./mvnw spring-boot:run
     ```

   - With Gradle:

     ```bash
     ./gradlew bootRun
     ```

   - Or by running the generated jar:

     ```bash
     java -jar target/*.jar
     ```

4. **Next steps**

   - Add more details about the Lovable.dev setup (frontend, environments, deployment).
   - Document environment variables and any external services (databases, APIs).
   - Describe how to run tests and how to contribute.


