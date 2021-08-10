# Day 1:
## AWS
### Amazon Web Services (AWS)

## Deploy an API to AWS Manually
AWS provides documentation on how to create a serverless web application utilizing RESTful API’s.

### Architecture Overview



### Steps
Create a new REST API
In the AWS Management Console, click Services then select API Gateway under Application Services.
Choose Create API.
Select New API and enter `WildRydes` for the API Name.
Keep `Edge optimized` selected in the Endpoint Type dropdown. Note: Edge optimized are best for public services being accessed from the Internet. Regional endpoints are typically used for APIs that are accessed primarily from within the same AWS Region.
Choose Create API
Create a Cognito User Pools Authorizer
Amazon API Gateway can use the JWT tokens returned by Cognito User Pools to authenticate API calls. In this step you'll configure an authorizer for your API to use the user pool you created in Module 2.
In the Amazon API Gateway console, create a new Cognito user pool authorizer for your API. Configure it with the details of the user pool that you created in the previous module. You can test the configuration in the console by copying and pasting the auth token presented to you after you log in via the /signin.html page of your current website.
Under your newly created API, choose Authorizers.
Chose Create New Authorizer.
Enter WildRydes for the Authorizer name.
Select Cognito for the type.
In the Region drop-down under Cognito User Pool, select the Region where you created your Cognito user pool in module 2 (by default the current region should be selected).
Enter WildRydes (or the name you gave your user pool) in the Cognito User Pool input.
Enter Authorization for the Token Source.
Choose Create.
Verify your authorizer configuration
Open a new browser tab and visit /ride.html under your website's domain.
If you are redirected to the sign-in page, sign in with the user you created in the last module. You will be redirected back to /ride.html.
Copy the auth token from the notification on the /ride.html,
Go back to previous tab where you have just finished creating the Authorizer
Click Test at the bottom of the card for the authorizer.
Paste the auth token into the Authorization Token field in the popup dialog.
Click Test button and verify that the response code is 200 and that you see the claims for your user displayed.
Create a new resource and method


Deploy your API
From the Amazon API Gateway console, choose Actions, Deploy API. You'll be prompted to create a new stage. You can use prod for the stage name.
In the Actions drop-down list select Deploy API.
Select [New Stage] in the Deployment stage drop-down list.
Enter `prod` for the Stage Name.
Choose Deploy.
Note the Invoke URL. You will use it in the next section.
Update the website configuration
Validate your implementation

(source: https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/module-4/)


## AWS Global Infrastructure

## Regions and Availability Zones 
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.RegionsAndAvailabilityZones.html.

1.	Regions and Availability zones 
Amazon cloud computing resources are hosted in multiple locations world-wide. These locations are composed of AWS Regions, Availability Zones, and Local Zones. Each AWS Region is a separate geographic area. Each AWS Region has multiple, isolated locations known as Availability Zones.
By using Local Zones, you can place resources, such as compute and storage, in multiple locations closer to your users. Amazon RDS enables you to place resources, such as DB instances, and data in multiple locations. Resources aren't replicated across AWS Regions unless you do so specifically.
Amazon operates state-of-the-art, highly-available data centers. Although rare, failures can occur that affect the availability of DB instances that are in the same location. If you host all your DB instances in a single location that is affected by such a failure, none of your DB instances will be available.
It is important to remember that each AWS Region is completely independent. Any Amazon RDS activity you initiate (for example, creating database instances or listing available database instances) runs only in your current default AWS Region. The default AWS Region can be changed in the console, by setting the AWS_DEFAULT_REGION environment variable, or it can be overridden by using the --region parameter with the AWS Command Line Interface (AWS CLI). For more information, see Configuring the AWS Command Line Interface, specifically the sections about environment variables and command line options.
Amazon RDS supports special AWS Regions called AWS GovCloud (US) that are designed to allow US government agencies and customers to move more sensitive workloads into the cloud. The AWS GovCloud (US) Regions address the US government's specific regulatory and compliance requirements. For more information, see What is AWS GovCloud (US)?
To create or work with an Amazon RDS DB instance in a specific AWS Region, use the corresponding regional service endpoint.

 
2.	Region availability
The following table shows the AWS Regions where Amazon RDS is currently available and the endpoint for each Region.
Region Name	Region	Endpoint	Protocol
US East (Ohio)	us-east-2	rds.us-east-2.amazonaws.com
rds-fips.us-east-2.amazonaws.com	HTTPS
HTTPS
US East (N. Virginia)	us-east-1	rds.us-east-1.amazonaws.com
rds-fips.us-east-1.amazonaws.com	HTTPS
HTTPS
US West (N. California)	us-west-1	rds.us-west-1.amazonaws.com
rds-fips.us-west-1.amazonaws.com	HTTPS
HTTPS
US West (Oregon)	us-west-2	rds.us-west-2.amazonaws.com
rds-fips.us-west-2.amazonaws.com	HTTPS
HTTPS
Africa (Cape Town)	af-south-1	rds.af-south-1.amazonaws.com	HTTPS
Asia Pacific (Hong Kong)	ap-east-1	rds.ap-east-1.amazonaws.com	HTTPS
Asia Pacific (Mumbai)	ap-south-1	rds.ap-south-1.amazonaws.com	HTTPS
Asia Pacific (Osaka)	ap-northeast-3	rds.ap-northeast-3.amazonaws.com	HTTPS
Asia Pacific (Seoul)	ap-northeast-2	rds.ap-northeast-2.amazonaws.com	HTTPS
Asia Pacific (Singapore)	ap-southeast-1	rds.ap-southeast-1.amazonaws.com	HTTPS
Asia Pacific (Sydney)	ap-southeast-2	rds.ap-southeast-2.amazonaws.com	HTTPS
Asia Pacific (Tokyo)	ap-northeast-1	rds.ap-northeast-1.amazonaws.com	HTTPS
Canada (Central)	ca-central-1	rds.ca-central-1.amazonaws.com
rds-fips.ca-central-1.amazonaws.com	HTTPS
HTTPS
Europe (Frankfurt)	eu-central-1	rds.eu-central-1.amazonaws.com	HTTPS
Europe (Ireland)	eu-west-1	rds.eu-west-1.amazonaws.com	HTTPS
Europe (London)	eu-west-2	rds.eu-west-2.amazonaws.com	HTTPS
Europe (Milan)	eu-south-1	rds.eu-south-1.amazonaws.com	HTTPS
Europe (Paris)	eu-west-3	rds.eu-west-3.amazonaws.com	HTTPS
Europe (Stockholm)	eu-north-1	rds.eu-north-1.amazonaws.com	HTTPS
Middle East (Bahrain)	me-south-1	rds.me-south-1.amazonaws.com	HTTPS
South America (São Paulo)	sa-east-1	rds.sa-east-1.amazonaws.com	HTTPS
AWS GovCloud (US-East)	us-gov-east-1	rds.us-gov-east-1.amazonaws.com	HTTPS
AWS GovCloud (US-West)	us-gov-west-1	rds.us-gov-west-1.amazonaws.com	HTTPS
If you do not explicitly specify an endpoint, the US West (Oregon) endpoint is the default.
When you work with a DB instance using the AWS CLI or API operations, make sure that you specify its regional endpoint.
Availability Zones
When you create a DB instance, you can choose an Availability Zone or have Amazon RDS choose one for you randomly. An Availability Zone is represented by an AWS Region code followed by a letter identifier (for example, us-east-1a).
You can't choose the Availability Zones for the primary and secondary DB instances in a Multi-AZ DB deployment. Amazon RDS chooses them for you randomly. For more information about Multi-AZ deployments, see High availability (Multi-AZ) for Amazon RDS.
Note
Random selection of Availability Zones by RDS doesn't guarantee an even distribution of DB instances among Availability Zones within a single account or DB subnet group. You can request a specific AZ when you create or modify a Single-AZ instance, and you can use more-specific DB subnet groups for Multi-AZ instances. For more information, see Creating an Amazon RDS DB instance and Modifying an Amazon RDS DB instance.
Local Zones
A Local Zone is an extension of an AWS Region that is geographically close to your users. You can extend any VPC from the parent AWS Region into Local Zones by creating a new subnet and assigning it to the AWS Local Zone. When you create a subnet in a Local Zone, your VPC is extended to that Local Zone. The subnet in the Local Zone operates the same as other subnets in your VPC.
When you create a DB instance, you can choose a subnet in a Local Zone. Local Zones have their own connections to the internet and support AWS Direct Connect. Thus, resources created in a Local Zone can serve local users with very low-latency communications. For more information, see AWS Local Zones.
A Local Zone is represented by an AWS Region code followed by an identifier that indicates the location, for example us-west-2-lax-1a.
Note
A Local Zone can't be included in a Multi-AZ deployment.
To use a Local Zone
1.	Enable the Local Zone in the Amazon EC2 console.
For more information, see Enabling Local Zones in the Amazon EC2 User Guide for Linux Instances.
2.	Create a subnet in the Local Zone.
For more information, see Creating a subnet in your VPC in the Amazon VPC User Guide.
3.	Create a DB subnet group in the Local Zone.
When you create a DB subnet group, choose the Availability Zone group for the Local Zone.
For more information, see Creating a DB instance in a VPC.
4.	Create a DB instance that uses the DB subnet group in the Local Zone.
For more information, see Creating an Amazon RDS DB instance.


## EC2/ Elastic Beanstalk
AWS Elastic Beanstalk
Definition:
AWS Elastic Beanstalk is an orchestration service offered by Amazon Web Services for deploying applications which orchestrates various AWS services, including EC2, S3, Simple Notification Service, CloudWatch, autoscaling, and Elastic Load Balancers. Wikipedia
AWS Elastic Beanstalk is an easy-to-use service for deploying and scaling web applications and services developed with Java, . NET, PHP, Node. js, Python, Ruby, Go, and Docker on familiar servers such as Apache, Nginx, Passenger, and IIS.
Elastic Beanstalk is one layer of abstraction away from the EC2 layer. Elastic Beanstalk will setup an "environment" for you that can contain a number of EC2 instances, an optional database, as well as a few other AWS components such as a Elastic Load Balancer, Auto-Scaling Group, Security Group.

---


# Day 2:
## Thread Class
The java.lang.Thread class is a thread of execution in a program. The Java Virtual Machine allows an application to have multiple threads of execution running concurrently. Every thread has a priority. Threads with higher priority are executed in preference to threads with lower priority. Each thread may or may not also be marked as a daemon.
 There are two ways to create a new thread of execution. One is to declare a class to be a subclass of Thread and the other way to create a thread is to declare a class that implements the Runnable interface

## Runnable Interface

Java runnable is an interface used to execute code on a concurrent thread. It is an interface which is implemented by any class if we want the instances of that class to be executed by a thread. The runnable interface has an undefined method run() with void as return type, and it takes in no arguments. It provides a standard set of rules for the instances of classes which wish to execute code when they are active. The most common use case of the Runnable interface is when we want only to override the run method. When a thread is started by the object of any class which is implementing Runnable, then it invokes the run method in the separately executing thread.

## Creating and executing threads - 
The following code would then create a thread and start it running:

     PrimeThread p = new PrimeThread(143);
     p.start();
 
The other way to create a thread is to declare a class that implements the Runnable interface. That class then implements the run method. An instance of the class can then be allocated, passed as an argument when creating Thread, and started. The same example in this other style looks like the following:

     class PrimeRun implements Runnable {
         long minPrime;
         PrimeRun(long minPrime) {
             this.minPrime = minPrime;
         }

         public void run() {
             // compute primes larger than minPrime
              . . .
         }
     }
 
The following code would then create a thread and start it running:

     PrimeRun p = new PrimeRun(143);
     new Thread(p).start();
 
Every thread has a name for identification purposes. More than one thread may have the same name. If a name is not specified when a thread is created, a new name is generated for it.
Unless otherwise noted, passing a null argument to a constructor or method in this class will cause a NullPointerException to be thrown.

## Making thread-safe singletons
Singleton is one of the most widely used creational design pattern to restrict the object created by applications. If you are using it in a multi-threaded environment, then the thread-safety of the singleton class is very important.

In real-world applications, resources like Database connections or Enterprise Information Systems (EIS) are limited and should be used wisely to avoid any resource crunch.

To achieve this, we can implement a Singleton design pattern. We can create a wrapper class for the resource and limit the number of objects created at runtime to one.

Thread Safe Singleton in Java
thread safe singleton in java
In general, we follow the below steps to create a singleton class:

Create the private constructor to avoid any new object creation with new operator.
Declare a private static instance of the same class.
Provide a public static method that will return the singleton class instance variable. If the variable is not initialized then initialize it or else simply return the instance variable.
Using the above steps I have created a singleton class that looks like below.

ASingleton.java

package com.journaldev.designpatterns;

public class ASingleton {

	private static ASingleton instance = null;

	private ASingleton() {
	}

	public static ASingleton getInstance() {
		if (instance == null) {
			instance = new ASingleton();
		}
		return instance;
	}

}

In the above code, the getInstance() method is not thread-safe.

Multiple threads can access it at the same time. For the first few threads when the instance variable is not initialized, multiple threads can enter the if loop and create multiple instances. It will break our singleton implementation.

How to achieve thread-safety in Singleton Class?
There are three ways through which we can achieve thread safety.

1.Create the instance variable at the time of class loading.

Pros:
Thread safety without synchronization
Easy to implement

Cons:
Early creation of resources that might not be used in the application.
The client application can’t pass any argument, so we can’t reuse it. For example, having a generic singleton class for database connection where client application supplies database server properties.

6.Synchronize the getInstance() method.

Pros:
Thread safety is guaranteed.
Client application can pass parameters
Lazy initialization achieved

Cons:
Slow performance because of locking overhead.
Unnecessary synchronization that is not required once the instance variable is initialized.

12.Use synchronized block inside the if loop and volatile variable

Pros:
Thread safety is guaranteed
Client application can pass arguments
Lazy initialization achieved
Synchronization overhead is minimal and applicable only for first few threads when the variable is null.

Cons:
Extra if condition

Looking at all the three ways to achieve thread-safety, I think the third one is the best option. In that case, the modified class will look like this:

package com.journaldev.designpatterns;

public class ASingleton {

	private static volatile ASingleton instance;
	private static Object mutex = new Object();

	private ASingleton() {
	}

	public static ASingleton getInstance() {
		ASingleton result = instance;
		if (result == null) {
			synchronized (mutex) {
				result = instance;
				if (result == null)
					instance = result = new ASingleton();
			}
		}
		return result;
	}

}

The local variable result seems unnecessary. But, it’s there to improve the performance of our code. In cases where the instance is already initialized (most of the time), the volatile field is only accessed once (due to “return result;” instead of “return instance;”). This can improve the method’s overall performance by as much as 25 percent.

If you think there are better ways to achieve this or if the thread-safety is compromised in the above implementation, please comment and share it with all of us.

Bonus Tip
String is not a very good candidate to be used with synchronized keyword. It’s because they are stored in a string pool and we don’t want to lock a string that might be getting used by another piece of code. So I am using an Object variable. Learn more about synchronization and thread safety in java.

## Thread API
java.lang
Class Thread
java.lang.Object
java.lang.Thread
All Implemented Interfaces:Runnable
Direct Known Subclasses:ForkJoinWorkerThread

public class Thread
extends Object
implements Runnable

## Thread States
A thread state. A thread can be in one of the following states:

NEW
A thread that has not yet started is in this state.

RUNNABLE
A thread executing in the Java virtual machine is in this state.

BLOCKED
A thread that is blocked waiting for a monitor lock is in this state.

WAITING
A thread that is waiting indefinitely for another thread to perform a particular action is in this state.

TIMED_WAITING
A thread that is waiting for another thread to perform an action for up to a specified waiting time is in this state.

TERMINATED
A thread that has exited is in this state.
A thread can be in only one state at a given point in time. These states are virtual machine states which do not reflect any operating system thread states.



## Producers and Consumers

Java EE CDI introduced a concept called Producer. Producers may be used to create - or produce - bean instances to be consumed by an application. Producers are also able to provide specific interface implementations according to the consumer needs so they are a valid way to support polymorphism in a CDI application.

Producers are also useful to encapsulate bean initialization or even to enable injection of object instances that are not themselves CDI managed beans into some points of our application.

The Consumer Interface is a part of the java.util.function package which has been introduced since Java 8, to implement functional programming in Java. It represents a function which takes in one argument and produces a result. However these kinds of functions don’t return any value.
Hence this functional interface which takes in one generic namely:-
T: denotes the type of the input argument to the operation
The lambda expression assigned to an object of Consumer type is used to define its accept() which eventually applies the given operation on its argument. Consumers are useful when it is not needed to return any value as they are expected to operate via side-effects.
## Producer/Consumer Problem
In computing, the producer-consumer problem (also known as the bounded-buffer problem) is a classic example of a multi-process synchronization problem. The problem describes two processes, the producer and the consumer, which share a common, fixed-size buffer used as a queue. 
The producer’s job is to generate data, put it into the buffer, and start again.
At the same time, the consumer is consuming the data (i.e. removing it from the buffer), one piece at a time.
Problem 
To make sure that the producer won’t try to add data into the buffer if it’s full and that the consumer won’t try to remove data from an empty buffer.
Solution 
The producer is to either go to sleep or discard data if the buffer is full. The next time the consumer removes an item from the buffer, it notifies the producer, who starts to fill the buffer again. In the same way, the consumer can go to sleep if it finds the buffer to be empty. The next time the producer puts data into the buffer, it wakes up the sleeping consumer. 
An inadequate solution could result in a deadlock where both processes are waiting to be awakened.
Implementation of Producer Consumer Class 
A LinkedList list – to store list of jobs in queue.
A Variable Capacity – to check for if the list is full or not
A mechanism to control the insertion and extraction from this list so that we do not insert into list if it is full or remove from it if it is empty.

## Callable Interface
Callable l vs Runnable Interfaces

Runnable vs Callable Interfaces in Java:
The Callable interface is similar to Runnable, in that both are designed for classes whose instances are potentially executed by another thread (multiThreading). 
A Runnable, however, does not return a result and cannot throw a checked exception.
Nb.  
-Runnable: Core interface provided for representing multi-thread tasks
-Callable: improved version of runnable added in Java 1.5

Differences:
1. Execution
	Both are Designed to represent tasks that can be executed by multiple threads i.e however
		i. Runnable: can be run using either the 'Thread' class or 'ExecutorService'. e.g 
				public interface Runnable{
					public void run(); 
				}

		ii. Callable: is Run using the 'ExecutorService'. e.g 
				public interface Callable<V>{
					V call() throws Exception();
				}
	
2. Return Values.
		Runnable: Single run() method. No Parameters passed, No values Returned.
		Callable:  Single call() method. Generic interface which returns a generic value.
		
3. Exception Handling:
		Runnable: Method does not have any " throws" exception specified, and therefore will not propagate any results
		Callable: includes "throws Exception" clauses  and will propagate additional exceptions, and return values.
		
		
		
    



## Future

The Future class represents a future result of an asynchronous computation – a result that will eventually appear in the Future after the processing is complete.
Long running methods are good candidates for asynchronous processing and the Future interface. This enables us to execute some other process while we are waiting for the task encapsulated in Future to complete.
Some examples of operations that would leverage the async nature of Future are:
computational intensive processes (mathematical and scientific calculations)
manipulating large data structures (big data)
remote method calls (downloading files, HTML scraping, web services).


## CompletableFuture
A CompletableFuture is a class used for asynchronous programming. It belongs to java.util.concurrent package, and implements CompletionStage and Future interface.
CompletionStage
It performs an action and returns a value when another completion stage completes.
A model for a task that may trigger other tasks.
Hence, it is an element of a chain. When more than one thread attempts to complete, complete exceptionally or cancel a CompletableFuture, only one of them succeeds.
Future has so many limitations, that's why we have CompletableFuture. It provides a broad set of methods for creating multiple Futures, chaining, and combining. It also has comprehensive exception handling support.
Creating a CompletableFuture
CompletableFuture<String> CompletableFuture = new CompletableFuture<String>();  


## Executor
public interface Executor
An object that executes submitted Runnable tasks. This interface provides a way of decoupling task submission from the mechanics of how each task will be run, including details of thread use, scheduling, etc. An Executor is normally used instead of explicitly creating threads. For example, rather than invoking new Thread(new(RunnableTask())).start() for each of a set of tasks, you might use:
 
Executor executor = anExecutor;
 executor.execute(new RunnableTask1());
 executor.execute(new RunnableTask2());
 
However, the Executor interface does not strictly require that execution be asynchronous. In the simplest case, an executor can run the submitted task immediately in the caller's thread. More typically, tasks are executed in some thread other than the caller's thread. Many Executor implementations impose some sort of limitation on how and when tasks are scheduled. 
 
The Executor implementations provided in this package implement ExecutorService, which is a more extensive interface. The Executors class provides convenient factory methods for these Executors.

## java.util.concurrent
Java Concurrency package covers concurrency, multithreading, and parallelism on the Java platform. Concurrency is the ability to run several or multi programs or applications in parallel. The backbone of Java concurrency are threads (a lightweight process, which has its own files and stacks and can access the shared data from other threads in the same process). The throughput and the interactivity of the program can be improved by performing time-consuming tasks asynchronously or in parallel

Java 5 added a new package to the java platform ⇾ java.util.concurrent package. This package has a set of classes and interfaces that helps in developing concurrent applications (multithreading) in java. Before this package, one needs to make the utility classes of their need on their own. 
