# Stage 1: Build the application
FROM openjdk:11 AS BUILD_IMAGE

LABEL "project"="vprofile"
LABEL "Author"="valery"

# Install Maven
RUN apt-get update && apt-get install -y maven git

# Clone the repository
RUN git clone https://github.com/envyvalery/vprofile-project.git

# Build the project
WORKDIR /vprofile-project
RUN mvn clean install

# Stage 2: Deploy the application to Tomcat
FROM tomcat:9-jre11

# Copy the built WAR file to the Tomcat webapps directory
COPY --from=BUILD_IMAGE /vprofile-project/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war

# Expose the Tomcat port
EXPOSE 8080

# Run Tomcat
CMD ["catalina.sh", "run"]
