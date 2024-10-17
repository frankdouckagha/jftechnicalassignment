## Pipeline with Jenkins
This project includes a Jenkins pipeline to automate the build, test, and packaging of the Spring PetClinic app. The Jenkinsfile is available in this repo 

### Steps Performed in the Pipeline

1. **Source Code**: Clones the Spring PetClinic source code from GitHub.
2. **Compile Code**: Uses Maven to compile the project.
3. **Run Tests**: Executes unit tests using Maven.
4. **Package as JAR**: Packages the project into a JAR file.
5. **Build Docker Image**: Builds a Docker image for the Spring PetClinic app.
6. **Push Docker Image**: Pushes the Docker image to JFrog Artifactory.

### Dependency Resolution

Originally, it was requested that dependencies be resolved from JCenter. However, since JCenter has been sunset, **Maven Central** is used as the dependency repository in this project.

### Running the Docker Image

Once the Docker image is pushed to artifactory, we can run it locally with the command:

```bash
docker run -p 8081:8080 jftest2.jfrog.io/jftest2-docker/spring-petclinic:<IMAGE_TAG>

Replace <IMAGE_TAG> with the actual image tag (The latest image tag is 3)

Once the Docker container is running, we can access the Spring PetClinic app on our browser with URL:

http://localhost:8081

This will bring up the Spring PetClinic homepage. 

