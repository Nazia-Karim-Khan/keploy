# Use a base image that has Java
FROM openjdk:17-jdk-slim

# Set the working directory
WORKDIR /app

RUN apt-get update && apt-get install -y curl

# Copy the JAR file
COPY target/spring-boot-demo-0.0.1-SNAPSHOT.jar app.jar

# Download the ca.crt file
 RUN curl -o ca.crt  https://raw.githubusercontent.com/keploy/keploy/refs/heads/main/pkg/core/proxy/tls/asset/ca.crt
 RUN curl -o setup_ca.sh https://raw.githubusercontent.com/keploy/keploy/refs/heads/main/pkg/core/proxy/tls/asset/setup_ca.sh
 # Give execute permission to the setup_ca.sh script
 RUN chmod +x setup_ca.sh


# Expose the port the app runs on
EXPOSE 8080

# Run the application
# ENTRYPOINT ["java", "-jar", "app.jar"]
ENTRYPOINT ["/bin/bash", "-c", "./setup_ca.sh && java -jar app.jar"]