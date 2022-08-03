# Web-Applications-Build-and-Deploy-Exercise
Web Applications Build and Deploy Exercise

Web Applications Build and Deploy Exercise

1.	Go over to spring initializr and create your project: https://start.spring.io/
a.	Under project select: Maven project
b.	Under Language select: Java
c.	Under Spring Boot select: 2.7.2 (Highest version that is not (SNAPSHOT or RC1)
d.	Under Project Metadata, for artifact enter: jfs_docker
e.	Under Packaging select: Jar
f.	Under Java select your version of Java: 18
g.	Click Add Dependencies and select: Spring Web.
h.	Click: GENERATE
i.	Or you can use this pre-initialized project

 


2.	Open your zip folder and copy it to your desktop or wherever you keep your projects (make sure you unzip the folder).

3.	Open your IntelliJ or any other IDE and select Open.

4.	Navigate to where you copied your jfs_docker project and select it, then click OK. Click Trust Project.

5.	Locate your package com.example.jfs_docker and create a Class named StudentController.

6.	Your StudentController class should have the @RestController annotation.

7.	Your StudentController class should have the @RequestMapping annotation.

8.	Add the following path to your RequestMapping annotation: path = “student”

9.	Your StudentController class should have one method that does the following:
a.	Should be public and have return type of String.
b.	Should be named sayHello()
c.	Should return the message “Hello Docker”
d.	Make sure to add the @GetMapping annotation to your method.

10.	 In your src/ directory, add a frontend/build/ directory

11.	 Inside the src/frontend/build/ directory, add an index.html file

12.	 Add an <h1> element to your index.html that says “Check out the /student endpoint!”

13.	In your pom.xml, add the below code just before the closing </project> tag

<profiles>
   <profile>
      <id>build-frontend</id>
      <activation>
         <activeByDefault>true</activeByDefault>
      </activation>
      <build>
         <plugins>
            <plugin>
               <artifactId>maven-resources-plugin</artifactId>
               <executions>
                  <execution>
                     <id>copy-build-folder</id>
                     <phase>process-classes</phase>
                     <goals>
                        <goal>copy-resources</goal>
                     </goals>
                     <configuration>
                        <resources>
                           <resource>
                              <directory>src/frontend/build</directory>
                           </resource>
                        </resources>
                        <outputDirectory>${basedir}/target/classes/static</outputDirectory>
                     </configuration>
                  </execution>
               </executions>
            </plugin>
         </plugins>
      </build>
   </profile>
</profiles>

14.	 Now lets test your code to make sure it runs. Using the command “./mvnw clean install” create a .jar file of your project. If you have trouble using the command line for this step, you can use the maven plugin as shown below to run both commands.
  
15.	Run your jar file (“java -jar ./target/jfs_docker-0.0.1-SNAPSHOT.jar”) and go to http://localhost:8080 in your browser and verify that you see your index.html page. Then, check out the get mapped endpoint in your browser: http://localhost:8080/student You should see “Hello Docker” displayed on your screen. Stop your application from running once you see it working.

16.	Now we will work on creating a Docker image for your application. 


(You can use the search bar to find mvn package)


17.	If you look inside your target folder you should see that a .jar file has been created. It should be named something like: jfs_docker-0.0.1-SNAPSHOT.jar

18.	Create a new file in the root directory of your application and name it: Dockerfile 
(Make sure you capitalize the first letter and use lowercase letters for the rest)

19.	Place the following inside your Dockerfile (For the ADD command, make sure the file name after target/ matches your file name and 3rd argument for  ENTRYPOINT should match name from ADD):
FROM openjdk:18
LABEL maintainer="jfs.com"
ADD target/jfs_docker-0.0.1-SNAPSHOT.jar jfs_docker.jar
ENTRYPOINT ["java", "-jar", "jfs_docker.jar"]

20.	 Make sure you have Docker running on your machine. Click on your Docker Desktop shortcut to open up and sign in if you are not already signed in.

21.	To build your Docker image go to your terminal(mac) or command prompt(windows) and navigate to the root directory of your application. (use cd command)

22.	Once you’re in the root directory of your application, execute: docker build -t jfs_docker:latest .
	(Don’t forget to include the . at the end of your build command)

23.	 To check if your Docker image was built execute: docker images
	(You should see your Docker image listed)

24.	 To run our Docker image inside of a Docker container and map your port execute:
	docker run -p 8080:8080 jfs_docker
	(Your firewall may try to block, make sure you allow the application to run)

25.	 Now in your browser, go to http://localhost:8080/student You should see “Hello Docker” displayed on your screen. Once you verify your application is running you can go to Docker Desktop and click “stop” to stop your application from running. 


Deploy app to Heroku
Make sure you have an account with Heroku and make sure you have Heroku CLI installed. Open your command prompt and execute: heroku
(Should see your version. If you don't then you need to install Heroku CLI)

Go to "Documentation" and select "The Heroku CLI" and click on Download and install.

Select the appropriate version and click Download. Once the file has downloaded open it and follow the instructions.

Close all your terminals and the re-open your terminal and execute: heroku
(You should see a list of commands)

(Do not use Git Bash on Windows, use Command Prompt if on Windows. Git Bash can get stuck after login sometimes)

1.	Create a system.properties file in the root directory of your application and add the following line: java.runtime.version=18
2.	Add the following to your ENTRYPOINT in your Dockerfile: “--server.port=${PORT}”
	 ENTRYPOINT ["java", "-jar", "jfs_docker.jar", "--server.port=${PORT}"]
	(Third argument “jfs_docker.jar” should be the name you used for your file)
3.	Go to Heroku and click on “New” “Create new app”
4.	Give your app a name, can be anything that isn’t already used. Select US and click “Create app”
5.	You should be at the Deploy page. Make sure “Heroku Git” is selected and follow the instructions.
	(When you execute “heroku login” you should see a login page open in your browser. If you don’t you can execute “heroku login -i” to log into heroku through your terminal rather than the browser)
(The last step, “git push heroku master” should be replaced with “git push heroku main”) Once the build is complete you should see a message with your url.
6.	Copy the URL for your deployed app and paste it in your address bar. After the .com enter your path “/student” (For example if your URL is “jfs-docker-app.com” you would enter “jfs-docker-app.com/student” in the address bar). You should see the message “Hello Docker” displayed on the screen.
7.	Once you’ve completed this exercise create a GitHub repository and push your code there. Share the link to your repository in the discussion forum in Canvas.
