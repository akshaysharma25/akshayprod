# Stage 1: Build the application
FROM openjdk:11 AS BUILD_IMAGE
RUN apt-get update -y && apt-get install git -y
RUN apt-get install maven -y
WORKDIR /home
COPY vprofile-project-local-setup /home/vprofile-project-local-setup
RUN cd vprofile-project-local-setup && mvn install

# Stage 2: Create the final image with Tomcat
FROM tomcat:9.0.78-jdk8-corretto-al2
WORKDIR /usr/local/tomcat
RUN rm -rf /webapps/*
COPY --from=BUILD_IMAGE /home/vprofile-project-local-setup/target/vprofile-v2.war /usr/local/tomcat/webapps/ROOT.war 
EXPOSE 8080
CMD ["catalina.sh", "run"]
