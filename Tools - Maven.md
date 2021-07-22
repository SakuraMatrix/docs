# Maven 
Opinionated project management tool for build automation, dependency management, and other actions. Once installed, use with the `mvn` command. Allows for a project to be IDE agnostic. See the official Maven project for documentation: http://maven.apache.org/index.html as well as the mvn repository to find available libraries: https://mvnrepository.com/

The minimum `pom.xml` example:
```xml
<project>
	<modelVersion>4.0.0</modelVersion>
	<groupId>YourDomainName</groupId>
	<artifactId>YourProjectName</artifactId>
	<version>0.1.0</version>
</project>
```

## Example commands
Create a new Maven project with the quickstart archetype. Change groupId and artifactId arguments as needed:
>mvn archetype:generate

Or skip the setup and run the generator in one line:
>mvn archetype:generate -DgroupId=com.revature -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

Compile class files into target/classes
>mvn compile

Package project into a jar file in target
>mvn package

Remove target folder and compiled build
>mvn clean

## Build Lifecycle
Maven builds step through a series of phases sequentially:
- **validate** - validate the project is correct and all necessary information is available
- **compile** - compile the source code of the project
- **test** - test the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- **package** - take the compiled code and package it in its distributable format, such as a JAR.
- **verify** - run any checks on results of integration tests to ensure quality criteria are met
- **install** - install the package into the local repository, for use as a dependency in other projects locally
- **deploy** - done in the build environment, copies the final package to the remote repository for sharing with other developers and projects.

For example, running `mvn package` will first run validate, compile, and test.

## Dependency Management
Maven can not only manage imported libraries, but resolve transitive dependencies required for each. Simply including a dependency will be enough for Maven to search for all other required dependencies.

To include a dependency, search on [Maven Repository](https://mvnrepository.com/) for its groupId, artifactId, and version. Inlude these tags in a `<dependency></dependency>` element within a `<dependencies></dependencies>` block.

```xml
<project>

...

	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
</project>
# Apache Maven 
Opinionated project management tool for build automation, dependency management, and other actions. Once installed, use with the `mvn` command. Allows for a project to be IDE agnostic. See the official Maven project for documentation: http://maven.apache.org/index.html as well as the mvn repository to find available libraries: https://search.maven.org/

<br>

## Overview
Java started as a Unix-style project, and most of its tooling is CLI focused. This includes the JDK's `javac` which parses, links, optimizes, and compiles bytecode instructions for a JVM into `.class` files. These can then be bundled by the `jar` command into an archived artifact. The JDK also has `javadoc` which parses source code for javadoc comments into a website for documentation. Furthermore, frameworks like JUnit have CLI runners that can parse a project for Test classes and methods.

However, when a project grows in size and complexity, so too does the CLI command arguments. In the C Programming language (and the official JDK project) this is solved by `make`, which is not optimized for Java's unique class loading process or package structures. Apache `ant` was an alternative and much better suited for Java projects, but it shared a similar issue with `make`: dependency management.

The Java ecosystem makes use of many 3rd party libraries, which in turn make use of other 3rd party libraries. Over time, a Java project would have to include each and every `jar` artifact for these libraries either in their `javac` classpath arguments or in their `make`/`ant` scripts.

Maven solves the dependency issue in a declaritive fashion. The project revolves around a depdendency library where each 3rd party `jar` is referenced not by its path like in previous examples but by its unique identifiers: `groupId` and `artifactId`. These tags allow the developer to declare a single dependency, which Maven will not only find but also resolve any transitive dependencies as well. And if Maven can't find these dependencies in its local library, it will search and download them from an online library known as a Maven repository.

The `mvn` utility, like `make` and `ant` before it, also manages the build scripting process of our Java projects. Maven is generally invoked with one or more subcommands representing a phase in a project's build lifecycle, such as `mvn compile` or `mvn install`. There are also some utility plugins invoked by goals which are not part of the build lifecycle but serve some useful purpose nonetheless.

If a developer needs to customize their build process or add some useful tooling, they can use Maven's plugin system to configure existing plugins or add additional plugins to their Maven project.

<br>

## Project Object Model
The `mvn` utility expects to read a project's configuration from a `pom.xml` file. This can be as simple as:

```xml
<project>
	<modelVersion>4.0.0</modelVersion>
	<groupId>YourDomainName</groupId>
	<artifactId>YourProjectName</artifactId>
	<version>0.1.0</version>
</project>
```
#### Example - Minimalistic `pom.xml`

But generally a `pom.xml` should include proper XML headers to help Maven and your IDE validate its tags and document structure properly:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	
    <modelVersion>4.0.0</modelVersion>
	<groupId>YourDomainName</groupId>
	<artifactId>YourProjectName</artifactId>
	<version>0.1.0</version>
</project>
```
#### Example - Proper `pom.xml` with headers

Even this is only a facade, and the full version can be viewed using the `mvn help:effective-pom` command.

<br>

## Project structure

Maven assumes a default project structure:
```
Project
├── pom.xml
└── src
    └── main
        └── java
            └── <Source Code>
```
But this can be changed to accomodate an existing project.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	
    <modelVersion>4.0.0</modelVersion>
	<groupId>YourDomainName</groupId>
	<artifactId>YourProjectName</artifactId>
	<version>0.1.0</version>
    
    <build>
		<directory>${project.basedir}/bin</directory>
		<outputDirectory>${project.build.directory}</outputDirectory>
		<sourceDirectory>${project.basedir}/src</sourceDirectory>
    </build>
</project>
```
#### Example - `pom.xml` with custom source directory

A `pom.xml` may also be generated from an existing template, known as a Maven Archetype:
>mvn archetype:generate

This will start an interactive process prompting the developer for project parameters and identifiers. To skip the setup and run the generator in one line:
```bash
mvn archetype:generate \
    -DgroupId=<YourDomainName> \
    -DartifactId=<YourProjectName> \
    -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Both options create a folder named after the `artifactId` with an automatically generated `pom.xml` and some placeholder classes in the standard Maven folder structure.

<br>

## Build Lifecycle
Maven builds step through a series of phases sequentially. Use `mvn help:describe -Dcmd=[phase]` to see a detailed list, but in general: 

- **validate** - validates the project is correct and all necessary information is available
- **compile** - compiles the source code of the project
- **test** - tests the compiled source code using a suitable unit testing framework. These tests should not require the code be packaged or deployed
- **package** - takes the compiled code and package it in its distributable format, such as a JAR.
- **verify** - runs any checks on results of integration tests to ensure quality criteria are met
- **install** - installs the package into the local repository, for use as a dependency in other projects locally
- **deploy** - copies the final package to the remote repository for sharing with other developers and projects.

For example, running `mvn package` will first run validate, compile, and test. To explore a plugin's goals, run `mvn help:describe -Dplugin=[plugin]`

<br>

## Dependency Management
To include a dependency, search the official [Maven Repository](https://search.maven.org/) for its `groupId`, `artifactId`, and `version`. Inlude these tags in a `<dependency></dependency>` element within a `<dependencies></dependencies>` block.

```xml
<project>
	<dependencies>
		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
			<scope>test</scope>
		</dependency>
	</dependencies>
</project>
```
#### Example - JUnit 4 dependency scoped to test lifecycle phase

A `scope` element can specify the lifecycle goal the dependency will be limited to. 

If a dependency is not available on Maven Central, a jar can be locally installed using the install command:
`mvn install:install-file -Dfile=<path-to-file> -DgroupId=<group-id> -DartifactId=<artifact-id> -Dversion=<version> -Dpackaging=<packaging>`

<br>

## Plugin Management
Maven plugins are a collection of goals, work units that accomplish an automated task. A basic Maven project will automatically include a number of plugins including the compiler plugin which can set the source and target value of the JDK version to use when compiling, and the surefire plugin which will automatically run JUnit tests found on the classpath.

These plugins can be configured within the `pom.xml`, and extra plugins can be added to introduce new automation tasks. These configurations should be wrapped by the `<build><plugins>...</plugins></build>` tags.

<br>

### Maven Clean Plugin
Like most plugins, the Clean plugin can be invoked with a <plugin>:<goal> pattern:
>mvn clean:clean

But as a core plugin, it has its own Lifecycle phase called `clean`:
>mvn clean

It can and should be used alongside other lifecycle phases:
>mvn clean package

<br>

### Maven Compiler Plugin
Like most plugins, the Compiler plugin can be invoked with a <plugin>:<goal> pattern:
>mvn compiler:compile

However, like the clean plugin it has its own Lifecycle phase:
>mvn compile

The Compiler plugin can be used to specify a project's target Java version (Maven assumes 1.5 by default), along with compiler arguments:
```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.1</version>
                <configuration>
                    <source>1.8</source>
                    <target>1.8</target>
                    <encoding>UTF-8</encoding>
                    <compilerArgs>
                        <arg>-g</arg>
                        <arg>-Xlint</arg>
                     </compilerArgs>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
#### Example - Maven Compiler Plugin configured for Java 8

It is also possible to simply add the configuration as a Maven property, foregoing the need to add a plugin configuration:
```xml
<project>
    <properties>
        <maven.compiler.source>1.8</maven.compiler.source>
        <maven.compiler.target>1.8</maven.compiler.target>
    </properties>
</project>
```
#### Example - Maven Compiler plugin configured through properties

<br>

### Maven Test Plugin
To run and display only a single test:
>mvn -q test -Dtest=[TestClass]#[method]
	
Tests can be skipped by adding `-DskipTests` to any normal lifecycle command.
	
<br>

### Maven Execution Plugin
To simplify the execution of a Java application, the exec plugin can be configured as follows:
```xml
<project>
    <build>
        <plugins>
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <configuration>
                    <mainClass>your.main.App</mainClass>
                    <commandlineArgs>Your Args</commandlineArgs>
                </configuration>
            </plugin>
        </plugins>
    </build>
</project>
```
#### Example - Maven Execution Plugin with main and args defined

And then the following command will run the plugin:
>mvn exec:java

Alternatively, the configuration element block can be removed while still using the plugin, or its arguments overwritten, with the following command:
>mvn exec:java -Dexec.mainClass="your.main.App" -Dexec.args="Your Args"

The execution plugin can also be configured through properties:
```xml
<properties>
	<exec.mainClass>your.main.App</exec.mainClass>
</properties>
```
#### Example - Maven Exec configured in properties

And the `mvn exec:java` command will run your program without any further plugin configuration. To suppress Maven log output, use the -q flag: `mvn -q exec:java`.

<br>

### Maven Assembly Plugin
While `mvn package` will bundle a project into a `jar` file, it does not bundle it with any dependencies. The Maven Dependency plugin and Maven Jar plugin may be used to copy dependencies into a folder and then bundle them with the final `jar`, but the Maven Assemply plugin can do both.

```xml
<project>
    <build>
        <plugins>
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <executions>
                    <execution>
                        <phase>package</phase>
                        <goals>
                            <goal>single</goal>
                        </goals>
                        <configuration>
                            <archive>
                                <manifest>
                                    <mainClass>your.main.App</mainClass>
                                </manifest>
                            </archive>
                            <descriptorRefs>
                                <descriptorRef>jar-with-dependencies</descriptorRef>
                            </descriptorRefs>
                        </configuration>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```
#### Example - Maven Assembly Plugin configured for self-executing uber-jar

This will copy any dependencies into the final `jar`, as well as add a Manifest file allowing the project to execute itself without Maven:
>java -jar target/output-jar-with-dependencies.jar
	
<br>

### Maven Versions Plugin
To change a project's version:
>mvn versions:set -DnewVersion=1.0.1-SNAPSHOT
	
To save this change:
>mvn versions:commit

## Resources
### Articles
- [A Short Guide to Maven](https://www.marcobehler.com/guides/mvn-clean-install-a-short-guide-to-maven)

### Books
- [Maven by Example](https://books.sonatype.com/mvnex-book/reference/index.html)

### Documentation
- [Maven Documentation](https://maven.apache.org/guides/index.html)

### Tutorials
- [Maven Getting Started Guide](https://maven.apache.org/guides/getting-started/index.html)
- [Maven for building Java applications](https://www.vogella.com/tutorials/ApacheMaven/article.html)
