Setup React Development Environment using NPM and create-react-app with builtin Tomcat server.

This project was build using the following link:
http://matejsprogblog.blogspot.com/2017/06/creating-new-web-app-using-create-react.html

To build the front end: use the following commands:
```
npm install -g create-react-app
create-react-app boot-react-example
use npm start  (start front end app)
```
check localhost:3000

To build the backend: 
create BootReactExample and GreetingController in main/java directory.
add sprint boot support in maven pom.xml.

```
 <build>
  <plugins>
   <plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
   </plugin>   
  </plugins>
 </build>
 ```

Since the front/backend application is different port, add proxy to the package.json
```
mvn clean package && java -jar target/boot-react-example-0.0.1-SNAPSHOT.jar
or 
mvn spring-boot:run (run without build)
```
check localhost:8080/greet for backend application to return "hello world"
 
To merge projects into one application with nodes, we use maven.
see pom.xml for frontend support in maven pom.xml

```
<build>
 <plugins>
  <plugin>
   <groupId>org.springframework.boot</groupId>
   <artifactId>spring-boot-maven-plugin</artifactId>
  </plugin>   
  <plugin>
   <groupId>com.github.eirslett</groupId>
   <artifactId>frontend-maven-plugin</artifactId>
   <version>1.4</version>
   <executions>
    <execution>
     <id>Install node and npm locally to the project</id>
     <goals>
      <goal>install-node-and-npm</goal>
     </goals>
     <configuration>
      <nodeVersion>v8.0.0</nodeVersion>
      <npmVersion>5.0.3</npmVersion>
     </configuration>
    </execution>
    <execution>
     <id>npm install</id>
     <goals>
      <goal>npm</goal>
     </goals>
    </execution>
    <execution>
     <id>Build frontend</id>
     <goals>
      <goal>npm</goal>
     </goals>
     <configuration>
      <arguments>run build</arguments>
     </configuration>
    </execution>
   </executions>
  </plugin> 
  <plugin>
   <groupId>org.apache.maven.plugins</groupId>
   <artifactId>maven-resources-plugin</artifactId>
   <executions>
    <execution>
     <id>Copy frontend build to target</id>
     <phase>process-resources</phase>
     <goals>
      <goal>copy-resources</goal>
     </goals>
     <configuration>
      <outputDirectory>${basedir}/target/classes/resources</outputDirectory>
      <resources>
       <resource>
        <directory>${basedir}/build</directory>
        <filtering>true</filtering>
       </resource>
      </resources>
     </configuration>
    </execution>
   </executions>
  </plugin>
 </plugins>
 </build>
```

Since the front/backend application is on same site, comment or get rid of the proxy in the package.json.
note: modify the App.js to call backend using fetch command. (see App.js for detail)
```
mvn clean package
cd target
java -jar target/boot-react-example-0.0.1-SNAPSHOT.jar
```
check localhost:8080 for the "hello world" message send from the backend application.
