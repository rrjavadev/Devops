# How to set up Docker file for a spring boot 

Here's an example Dockerfile to create an image of a Spring Boot application:

```
# Use a Java runtime as a base image
FROM openjdk:8-jdk-alpine

# Set the working directory to /app
WORKDIR /app

# Copy the Spring Boot application JAR file into the container at /app
COPY target/my-spring-boot-app.jar /app

# Expose port 8080 to the outside world
# To expose a port in a Dockerfile, you can use the EXPOSE instruction. 
# This instruction informs Docker that the container will listen on the 
# specified network port(s) at runtime.

# Here's the syntax of the EXPOSE instruction:
EXPOSE 8080

# Run the Spring Boot application when the container starts
CMD ["java", "-jar", "my-spring-boot-app.jar"]

```

### This Dockerfile does the following:

1. Starts with a base image of the Java runtime that includes the JDK and is optimized for Alpine Linux.

2. Sets the working directory of the container to /app.

3. Copies the Spring Boot application JAR file (assuming it's already been built) into the container at /app.

4. Exposes port 8080, which is the default port used by Spring Boot applications.

5. Defines the command to run the Spring Boot application, which starts the 
Java runtime and runs the JAR file using the "java -jar" command.

To use this Dockerfile, you would need to navigate to the directory containing the Dockerfile and the Spring Boot application JAR file and run the following command:

```
docker build -t my-spring-boot-app-image .
```

This command builds a Docker image using the Dockerfile and tags it with the name "my-spring-boot-app-image". The "." at the end of the command specifies that the Dockerfile is in the current directory. Once the image is built, you can run a container based on the image using the "docker run" command. 

```
docker run -p 8080:8080 <image-name>
```
Replace <image-name> with the name of the Docker image you want to run.

Note that exposing a port in the Dockerfile does not actually publish the port to the host; it only informs Docker that the container will listen on that port at runtime. You still need to use the -p or --publish option when running the container to bind the exposed port to a host port.

Use the following command to list all the Docker images on your system:
```
docker images
```

Use the following command to delete the image:

```
docker rmi [IMAGE ID]
```
Replace [IMAGE ID] with the ID of the image you want to delete. You can also specify the repository and tag instead of the ID, like this:

```
docker rmi [REPOSITORY]:[TAG]
```

For example, if you wanted to delete an image with the repository name "my-app" and the tag "latest", you would use the following command:

```
docker rmi my-app:latest
```


If the image has dependent child images or running containers, you can use the "-f" or "--force" option to force the removal of the image:

```
docker rmi -f [IMAGE ID]
```

Be careful when using the "-f" option, as it will forcibly remove the image without checking for dependent child images or running containers.

After executing the command, Docker will delete the specified image and any dependent child images that are no longer needed.

Finally, to stop all the running containers, use the following command.

```
 docker stop $(docker ps -q)
```

If you only want to stop a specific container, you can replace $(docker ps -q) with the ID or name of the container you want to stop, like this:

```
docker stop <container-id-or-name>
```

Replace <container-id-or-name> with the actual ID or name of the container you want to stop.



