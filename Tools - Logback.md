# Logback and how to configure it.
This should be a simplified way to help you guys configure the logger that comes with logback. Plus, it doesn't require you to read through the Logback docs just to get started with the basics. I do still recommend reading them, however, as there are some things in there that are very useful to know that I don't go into enough detail on.

## Step 0: Decide if you want to automate the config, or do it manually
You can either use a config file or set up the configuration directly in your code. I will show you how to set it up using the config file.

## Step 1: Include logback in your pom.xml
```
<dependency>
  <groupId>ch.qos.logback</groupId>
  <artifactId>logback-classic</artifactId>
  <version>1.2.3</version>
</dependency>
```

## Step 2: Create the config file
So the documentation requires you to create a file titled one of the following:
- logback-test.xml
- logback.groovy
- logback.xml
Or if you don't have such file, a service-provider loading facility is used. If you don't have that, then it auto-configures itself so you can at least use it.

**Note**:
***THIS FILE MUST BE IN EITHER main/java/resources or directly in the classpath (no subfolders) of your program for it to be read***

## Step 3: Configure the config file
After creating the config file, you now have the ability to configure Logback.
### For printing to a file you would do something like this:
```
<appender name="FILE" class="ch.qos.logback.core.FileAppender">
  <File>YOUR FILE NAME GOES HERE.log</File>
  <encoder>
    <Pattern>%d %p %t %c - %m%n</Pattern>
  </encoder>
</appender>        
```
### And for printing to the console, it would look like this:
```
<appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">
  <encoder>
    <pattern>%msg%n</pattern>
  </encoder>
</appender>
  ```
## Step 4: Creating Loggers:
Creating the appenders for I/O is the first step of fully using Logback. Now you have to name the loggers.

To do this, all you have to do is include the ```<logger>``` tag after you finish declaring all of your appenders.
The naming scheme of your loggers has an effect on how they behave. For example, I have a logger named *logger*. This *logger* outputs to the console and is declared in the XML
like so:
```
<logger name="logger">
  <appender-ref ref="STDOUT"/>
</logger>
```

Now *logger* has a child that has the name *logger.driver*. *logger.driver* ***inherits*** all tags and settings that *logger* had when it was declared, in addition to any that *logger.driver* may declare itself, including to the same output. There are ways to avoid this additive effect but you should read the docs for that.
  
 ## Step 5: Finish the config file:
 At the bottom of your document, you need to include the root level that all of your loggers inherit behavior from.
 That looks like this:
 ```
<root level="debug">
  <appender-ref ref="APPENDER NAME GOES HERE"/>
</root>
```

After that, all you need to do is run your program and it starts keeping track of your logs!

## Links to the documentation
- Architecture
  - http://logback.qos.ch/manual/architecture.html
- Configuration 
  - http://logback.qos.ch/manual/configuration.html
- FAQ
  - http://logback.qos.ch/faq.html
- Error Code Reference Sheet
  - http://logback.qos.ch/codes.html
 
 ## Example config file:
 This is my config file for my project 0 to act as an example of a full config file.
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
