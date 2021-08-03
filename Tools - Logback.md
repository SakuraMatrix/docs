# Logback and how to configure it
This is a simplified guide to configure the logger that comes with Logback that does not require reading through the Logback documentation to get started with the basics. I do still recommend reading them however, as there is useful content that I do not go into enough detail on in this guide.

## Step 0: Decide if you want to automate the configuration, or do it manually
You can either use a configuration file or set up the configuration directly in your code. This guide focuses on setting it up using the configuration file.

## Step 1: Include Logback in your pom.xml
Add the following snippet to the dependencies list of your POM.
```
<dependency>
  <groupId>ch.qos.logback</groupId>
  <artifactId>logback-classic</artifactId>
  <version>1.2.3</version>
</dependency>
```

## Step 2: Create the configuration file
The documentation requires you to create a file titled one of the following:
- logback-test.xml
- logback.groovy
- logback.xml

If no such files are found, a service-provider loading facility is used.

If none of the above are available, then Logback will configure itself automatically.

**NOTE**

***This file must be in either `main/java/resources` or directly in the classpath (no subfolders) of your program for it to be read***

## Step 3: Configure the configuration file
After creating the configuration file, you now have the ability to configure Logback.

### Example configuration for printing to a file
```
<appender name="FILE" class="ch.qos.logback.core.FileAppender">
  <File>YOUR FILE NAME GOES HERE.log</File>
  <encoder>
    <Pattern>%d %p %t %c - %m%n</Pattern>
  </encoder>
</appender>
```

### Example configuration for printing to the console
```
<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
  <encoder>
    <pattern>%msg%n</pattern>
  </encoder>
</appender>
```

## Step 4: Creating Loggers

Creating the appenders for I/O is the first step of using Logback; you must now name the loggers.

To do this, include the `<logger>` tag after you have finished declaring your appenders.

The naming scheme of your loggers has an effect on how they behave. For example, I have a logger named `logger`. This `logger` outputs to the console and is declared in the XML like so:
```
<logger name="logger">
  <appender-ref ref="STDOUT"/>
</logger>
```

Now `logger` has a child that has the name `logger.driver`. `logger.driver` ***inherits*** all tags and settings that `logger` has when it was declared, in addition to any that `logger.driver` may declare itself, including to the same output. There are ways to avoid this additive effect, the details of which are provided in the documentation.

## Step 5: Finish the configuration file:
Your loggers will all inherit behavior from the root level so you must include the root level at the bottom of your document. 

### Example
 ```
<root level="debug">
  <appender-ref ref="APPENDER NAME GOES HERE"/>
</root>
```

After that, all you will need to do is run your program and it will start keeping track of your logs!

## Links to the documentation
- Architecture
  - http://logback.qos.ch/manual/architecture.html
- Configuration
  - http://logback.qos.ch/manual/configuration.html
- FAQ
  - http://logback.qos.ch/faq.html
- Error Code Reference Sheet
  - http://logback.qos.ch/codes.html

## Example configuration file:
This is the configuration file for my project 0.
```
 <configuration debug="true">
    <appender name="FILE" class="ch.qos.logback.core.FileAppender">
        <File>events.log</File>
        <encoder>
            <Pattern>%d %p %t %c - %m%n</Pattern>
        </encoder>
    </appender>
    <logger name="logger"/>
    <logger name="logger.IO"/>
    <logger name="logger.Driver"/>
    <logger name="logger.Driver.Analyzer"/>
    <logger name="logger.Driver.Doc"/>
    <logger name="logger.IO.Validation"/>
    <root level="debug">
        <appender-ref ref="FILE"/>
    </root>
</configuration>
```
