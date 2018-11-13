This project was build using the following link:
http://matejsprogblog.blogspot.com/2017/06/creating-new-web-app-using-create-react.html

To build the front end: use the following commands:
>>npm install -g create-react-app

>>create-react-app boot-react-example

>>use npm start to start front end app.

>>check localhost:3000

This project was bootstrapped with [Create React App](https://github.com/facebook/create-react-app).

## Available Scripts

In the project directory, you can run:

### `npm start`

Runs the app in the development mode.<br>
Open [http://localhost:3000](http://localhost:3000) to view it in the browser.

The page will reload if you make edits.<br>
You will also see any lint errors in the console.

### `npm test`

Launches the test runner in the interactive watch mode.<br>
See the section about [running tests](https://facebook.github.io/create-react-app/docs/running-tests) for more information.

### `npm run build`

Builds the app for production to the `build` folder.<br>
It correctly bundles React in production mode and optimizes the build for the best performance.

The build is minified and the filenames include the hashes.<br>
Your app is ready to be deployed!

See the section about [deployment](https://facebook.github.io/create-react-app/docs/deployment) for more information.

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

If you aren’t satisfied with the build tool and configuration choices, you can `eject` at any time. This command will remove the single build dependency from your project.

Instead, it will copy all the configuration files and the transitive dependencies (Webpack, Babel, ESLint, etc) right into your project so you have full control over them. All of the commands except `eject` will still work, but they will point to the copied scripts so you can tweak them. At this point you’re on your own.

You don’t have to ever use `eject`. The curated feature set is suitable for small and middle deployments, and you shouldn’t feel obligated to use this feature. However we understand that this tool wouldn’t be useful if you couldn’t customize it when you are ready for it.

## Learn More

You can learn more in the [Create React App documentation](https://facebook.github.io/create-react-app/docs/getting-started).

To learn React, check out the [React documentation](https://reactjs.org/).

To build the backend: use the following commands:
>>create BootReactExample  and GreetingController in main/java directory.
>>add backend application support in maven pom.xml.

 <build>
  <plugins>
   <plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
   </plugin>   
  </plugins>
 </build>

>>since the front/backend application is different port, add proxy to the package.json 
>>mvn clean package && java -jar target/boot-react-example-0.0.1-SNAPSHOT.jar
>>check localhost:8080/greet for backend application to return "hello world"
 
To merge projects into one application with nodes, we use maven.
>>see pom.xml for frontend support in maven pom.xml
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

>>since the front/backend application is on same site, comment or get rid of the proxy in the package.json.

>>mvn clean package && java -jar target/boot-react-example-0.0.1-SNAPSHOT.jar

>>check localhost:8080 for the "hello world" message send from the backend application.
