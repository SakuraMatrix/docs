# Day 1:
## Amazon Web Services (AWS)
### Cloud Computing
Cloud computing is a collection of online managed services (especially data storage and computing power) owned, run, and maintained by a cloud provider, without direct active management from users. Pay for what you use.

#### Users
Organizations of any type, size, or industry use cloud computing. For example:
Mobile apps companies
Websites
Large organizations with extended IT services
Video streaming platforms Netflix, Hulu, youtube…
Online video games
Developers that need to work together in a shared environment

## Benefits of Cloud Computing
### Agility
The cloud is agile. Infrastructure resources can spin up when necessary. Among these resources are compute, storage, databases, Internet of things (IoT), machine learning, analytics, and more.

### Elasticity
The cloud has the ability to handle peak levels of business activity automatically and on-demand, by scaling resources up or down to shrink or grow capacity when the business needs change.

### Economy
Because cloud computing removes the traditional costs of owning and maintaining hardware, and payment is only for usage, the cost savings are very large. On top of that cloud computing providers offer steep discounts for some resources, such as compute, if the workflow on them can be interrupted. This even further increases the cost-savings of running in the cloud.

### Availability
Cloud computing providers offer their services in many locations within a geographical region, and in many locations around the globe. This extends the availability and durability of cloud services.

### Types of Cloud Computing
#### Infrastructure as a service (IaaS)
Infrastructure as a service (IaaS), also known as cloud infrastructure services, are highly scalable and automated computing resources.

IaaS is fully self-service for accessing and monitoring computers, networking, storage, and other services.

This model allows businesses to purchase resources on-demand and as-needed, instead of having to buy the hardware outright.

##### IaaS Characteristics
Resources are available as a service
Cost varies depending on consumption
Services are highly scalable
Multiple users share a single piece of hardware
Organization retain control of the infrastructure
Dynamic and flexible

#### Platform as a service (PaaS)
Platform as a service (PaaS), also known as cloud platform services, allows developers to build upon a framework to create custom applications. By obstructing or hiding servers, storage, and networking, PaaS providers help developers focus on managing their applications, rather managing the base infrastructure. Heroku is an example of a PaaS provider.

##### PaaS Characteristics
Builds on virtualization technology, so resources can easily be scaled up or down
Provides a variety of services to assist with the development, testing, and deployment of apps
Accessible to numerous users via the same development application
Integrates web services and databases

#### Software as a service (SaaS)
The most common option for cloud use, allowing 3rd-party vendors to deliver applications that run in the browser, without any installation. For example, G Suite is a SaaS solution for office apps in your browser.

##### SaaS characteristics:
Managed from a central location
Hosted on a remote server
Accessible in a browser (sometimes even when the user is offline)
Users are not responsible for hardware or software updates

### Cloud Deployment Models
#### Public Deployment
The Public Deployment model is the most common deployment model. Services face the Internet and share hardware, network, and storage across many organizations and tenants.

##### Advantages
Cost-effective
Pay-as-you-go - only pay for resources you use
Maintenance-free - the cloud provider is responsible

#### Private Deployment
The Private Deployment model limits each deployment to a single organization. This model provides better control of network security. Resources are not shared between organizations and tenants, which reduces risk.

The private cloud can be an on-premise or it can be hosted by a cloud provider. Even if the deployment is hosted by a cloud provider, all of the hardware and software is dedicated to one organization.

The Private Deployment model is often used by governments, financial institutions, or organizations that must comply with strict regulatory protocols

##### Advantages

Supports highly customized networks
Facilitates tighter security and privacy
Provides greater control over infrastructure

#### Hybrid Deployment
The Hybrid Deployment model is a mix of the Public and Private Deployment models, combining the benefits of both.

This model offers the flexibility of running on private infrastructure, but the model can switch to the public cloud when permissible, to realize the benefits such as cost-savings.

In Hybrid Deployment data can flow from the private cloud to the public cloud and vice versa.

The downside of a hybrid deployment model is the cost of configuring and maintaining services across both types of clouds.

### Costs In The Cloud
Cost savings is one of the reasons why companies are moving into the Cloud, but these costs can get out of hand easily.

Cloud providers supply up-to-date pricing information for all of their services and components.

Let's explore one way to estimate the costs for the infrastructure we need on AWS using the AWS Pricing Calculator.






###When Not to Use The Cloud
There are situations in which the costs of running in the cloud surpass the costs of running and maintaining a set of servers.

One example is GPU machine learning. While the cloud can provide cost optimization for GPU instances via spot instance discounts, often the cost of running a set of cloud GPU instances would be much higher than the cost to buy and maintain your own set of GPU servers.

Other examples include the Private deployment model, which might be on-premise for security or regulatory reasons.

Even though the cloud has many managed services, cloud applications still require an experienced engineer with security, networking, and cloud skills to maintain the application. If an organization lacks such a person, the cloud might not be a good option.






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
Create a new resource called /ride within your API. Then create a POST method for that resource and configure it to use a Lambda proxy integration backed by the RequestUnicorn function you created in the first step of this module.

In the left nav, click on Resources under your WildRydes API.
From the Actions dropdown select Create Resource.
Enter ride as the Resource Name.
Ensure the Resource Path is set to ride.
Select Enable API Gateway CORS for the resource.
Click Create Resource.
With the newly created /ride resource selected, from the Action dropdown select Create Method.
Select POST from the new dropdown that appears, then click the checkmark.
Select Lambda Function for the integration type.
Check the box for Use Lambda Proxy integration.
Select the Region you are using for Lambda Region.
Enter the name of the function you created in the previous module, RequestUnicorn, for Lambda Function.
Choose Save. Please note, if you get an error that you function does not exist, check that the region you selected matches the one you used in the previous module.
When prompted to give Amazon API Gateway permission to invoke your function, choose OK.
Choose on the Method Request card.
Choose the pencil icon next to Authorization.
Select the WildRydes Cognito user pool authorizer from the drop-down list, and click the checkmark icon.
Deploy your API
From the Amazon API Gateway console, choose Actions, Deploy API. You'll be prompted to create a new stage. You can use prod for the stage name.
In the Actions drop-down list select Deploy API.
Select [New Stage] in the Deployment stage drop-down list.
Enter `prod` for the Stage Name.
Choose Deploy.
Note the Invoke URL. You will use it in the next section.
Update the website configuration
Update the /js/config.js file in your website deployment to include the invoke URL of the stage you just created. You should copy the invoke URL directly from the top of the stage editor page on the Amazon API Gateway console and paste it into the _config.api.invokeUrl key of your sites /js/config.js file. Make sure when you update the config file it still contains the updates you made in the previous module for your Cognito user pool.

If you completed module 2 manually, you can edit the config.js file you have saved locally. If you used the AWS CloudFormation template, you must first download the config.js file from your S3 bucket. To do so, visit /js/config.js under the base URL for your website and choose File, then choose Save Page As from your browser.
Open the config.js file in a text editor.
Update the invokeUrl setting under the api key in the config.js file. Set the value to the Invoke URL for the deployment stage your created in the previous section.

An example of a complete config.js file is included below. Note, the actual values in your file will be different.

```
window._config = {
    cognito: {
        userPoolId: 'us-west-2_uXboG5pAb', // e.g. us-east-2_uXboG5pAb         
        userPoolClientId: '25ddkmj4v6hfsfvruhpfi7n4hv', // e.g. 25ddkmj4v6hfsfvruhpfi7n4hv
        region: 'us-west-2' // e.g. us-east-2 
    }, 
    api: { 
        invokeUrl: 'https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod' // e.g. https://rc7nyt4tql.execute-api.us-west-2.amazonaws.com/prod, 
    } 
};
```

Save your changes locally.
In the AWS Management Console, choose Services then select S3 under Storage.
Navigate to the website bucket and then browse to the js key prefix.
Choose Upload.
Choose Add files, select the local copy of config.js and then click Next.
Choose Next without changing any defaults through the Set permissions and Set properties sections.
Choose Upload on the Review section.
Validate your implementation
Note: It is possible that you will see a delay between updating the config.js file in your S3 bucket and when the updated content is visible in your browser. You should also ensure that you clear your browser cache before executing the following steps.

Visit /ride.html under your website domain.
If you are redirected to the sign in page, sign in with the user you created in the previous module.
After the map has loaded, click anywhere on the map to set a pickup location.
Choose Request Unicorn. You should see a notification in the right sidebar that a unicorn is on its way and then see a unicorn icon fly to your pickup location.

(Source: https://aws.amazon.com/getting-started/projects/build-serverless-web-app-lambda-apigateway-s3-dynamodb-cognito/module-4/)
(Source: https://www.udacity.com/course/intro-to-cloud-computing--ud080)


## AWS Global Infrastructure
### Major Cloud Providers
Amazon Web Services (AWS)
Google Cloud Platform (GCP)
Microsoft Azure
At a high level, these providers are similar. However, there are many factors that distinguish them from each other, including:
Geographic Availability
Market Share and Growth Rate
Services
Pricing Model

#### Geographic Availability
Cloud computing locations are worldwide. These locations called "regions" and "availability zones."

Each region is a separate geographic area. Within each region, there are multiple isolated locations known as availability zones.

This geographic spread provides the ability to place resources, such as compute and storage, closer to end-users for faster access and better performance.

The number of regions and the availability zones within them differs between cloud providers.

AWS has 18 regions and between 2-6 availability zones per region
GCP has 23 regions with at least 3 availability zones per region
Azure has 58 regions worldwide and is available in 140 countries all around the world
The geographic locations between each cloud providers are different. One example is that currently the only cloud provider that can work in mainland China is AWS GCP offers a region in Hong Kong, but those resources are not always accessible from mainland China.

And there are other key factors such as submarine networking between geographic locations.


#### Market Share And Growth Rate
AWS has been around since 2006 and is currently the leading cloud provider, with 33% market share
Microsoft Azure holds about 17% worldwide market share
Google has about 6% percent of the market worldwide
While this doesn't add up to 100%, remember that there are many other cloud providers that, in aggregate, make up the entire cloud computing market.

#### Services
AWS offers 200+ services, ranging from computing, storage, and databases through machine learning and artificial intelligence (AI) to Internet of Things (IoT), analytics, and more
GCP offers about 50+ services, similar to AWS
Azure offers about 30+ services, with a focus on integration with other Microsoft tools

#### Pricing
The pricing models of the major cloud provides are similar:


On-demand, pay-as-you-go
Discounts for committed usage
Usage-based serverless resources
On-demand pricing for the same compute (CPU-RAM-Disk) resources varies between cloud providers and is calculated on an hourly rate.

Discounts also vary between cloud providers. For example, AWS offers reserved instances that you can pre-purchase annually, whereas GCP offers "sustained use discount" whereby pricing goes down the more you use an instance.

Serverless computing (Lambda on AWS, Functions on Azure, and Cloud Functions on GCP) are billed for the compute power you use, based on 100-millisecond increments.





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
### Cloud History
In the early days of the Internet, before cloud computing, hosting providers allocated shared servers where one could run and install a monolithic app. This approach encountered challenges to scalability and resiliency, as well as security risks.

Cloud computing became popular in 2006, when Amazon.com released its "Elastic Cloud Compute" service, known as EC2 ('E' for elastic and 2 'C's for Cloud Compute). Cloud computing addresses many of the challenges faced by early application platforms.

The word "cloud" has long been a metaphor for the Internet, and the cloud symbol was used in network telephony schematics all the way back to the 1970s.

Since 2006, other cloud providers have surfaced. Additionally, many more services have been incorporated into the cloud, to minimize different self-managed services necessary to run different types of web applications.


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








# Day 3:
## Thread basics

https://beginnersbook.com/2013/03/java-threads/ 

	What are Java Threads?
A thread is a:
Facility to allow multiple activities within a single process
Referred as lightweight process
A thread is a series of executed statements
Each thread has its own program counter, stack and local variables
A thread is a nested sequence of method calls
Its shares memory, files and per-process state
 
Read: Multithreading in Java
What's the need of a thread or why we use Threads?
To perform asynchronous or background processing
Increases the responsiveness of GUI applications
Take advantage of multiprocessor systems
Simplify program logic when there are multiple independent entities
What happens when a thread is invoked?
When a thread is invoked, there will be two paths of execution. One path will execute the thread and the other path will follow the statement after the thread invocation. There will be a separate stack and memory space for each thread.
Risk Factor
Proper co-ordination is required between threads accessing common variables [use of synchronized and volatile] for consistence view of data
overuse of java threads can be hazardous to program’s performance and its maintainability.
 
Threads in Java
Java threads facility and API is deceptively simple:
Every java program creates at least one thread [ main() thread ]. Additional threads are created through the Thread constructor or by instantiating classes that extend the Thread class.
Thread creation in Java
Thread implementation in java can be achieved in two ways:
Extending the java.lang.Thread class
Implementing the java.lang.Runnable Interface
 
Note: The Thread and Runnable are available in the   java.lang.* package
1) By extending thread class
The class should extend Java Thread class.
The class should override the run() method.
The functionality that is expected by the Thread to be executed is written in the run() method.
void start(): Creates a new thread and makes it runnable.
void run(): The new thread begins its life inside this method.
Example:
public class MyThread extends Thread {
   public void run(){  
    System.out.println("thread is running...");  
  } 
   public static void main(String[] args) {
     MyThread obj = new MyThread();
     obj.start();
}
2) By Implementing Runnable interface
The class should implement the Runnable interface
The class should implement the run() method in the Runnable interface
The functionality that is expected by the Thread to be executed is put in the run() method
Example:
public class MyThread implements Runnable {
   public void run(){  
     System.out.println("thread is running..");  
   }  
   public static void main(String[] args) {
     Thread t = new Thread(new MyThread());
     t.start();
}
Extends Thread class vs Implements Runnable Interface?
Extending the Thread class will make your class unable to extend other classes, because of the single inheritance feature in  JAVA. However, this will give you a simpler code structure. If you implement Runnable, you can gain better object-oriented design and consistency and also avoid the single inheritance problems.
If you just want to achieve basic functionality of a thread you can simply implement Runnable interface and override run() method. But if you want to do something serious with thread object as it has other methods like suspend(), resume(), ..etc which are not available in Runnable interface then you may prefer to extend the Thread class.
Thread life cycle in java
Read full article at: Thread life cycle in java
Ending Thread
A Thread ends due to the following reasons:
The thread ends when it comes when the run() method finishes its execution.
When the thread throws an Exception or Error that is not being caught in the program.
Java program completes or ends.
Another thread calls stop() methods.
Synchronization of Threads
In many cases concurrently running threads share data and two threads try to do operations on the same variables at the same time. This often results in corrupt data as two threads try to operate on the same data.
A popular solution is to provide some kind of lock primitive.  Only one thread can acquire a particular lock at any particular time. This can be achieved by using a keyword “synchronized” .
By using the synchronize only one thread can access the method at a time and a second call will be blocked until the first call returns or wait() is called inside the synchronized method.
Deadlock
Whenever there is multiple processes contending for exclusive access to multiple locks, there is the possibility of deadlock. A set of processes or threads is said to be deadlocked when each is waiting for an action that only one of the others can perform.
In Order to avoid deadlock, one should ensure that when you acquire multiple locks, you always acquire the locks in the same order in all threads.
Guidelines for synchronization
Keep blocks short. Synchronized blocks should be short — as short as possible while still protecting the integrity of related data operations.
Don’t block. Don’t ever call a method that might block, such as InputStream.read(), inside a synchronized block or method.
Don’t invoke methods on other objects while holding a lock. This may sound extreme, but it eliminates the most common source of deadlock.
 

## Thread pool
	Thread Pools
http://tutorials.jenkov.com/java-concurrency/thread-pools.html
A thread pool is a pool threads that can be "reused" to execute tasks, so that each thread may execute more than one task. A thread pool is an alternative to creating a new thread for each task you need to execute.
Creating a new thread comes with a performance overhead compared to reusing a thread that is already created. That is why reusing an existing thread to execute a task can result in a higher total throughput than creating a new thread per task.
Additionally, using a thread pool can make it easier to control how many threads are active at a time. Each thread consumes a certain amount of computer resources, such as memory (RAM), so if you have too many threads active at the same time, the total amount of resources (e.g. RAM) that is consumed may cause the computer to slow down - e.g. if so much RAM is consumed that the operating system (OS) starts swapping RAM out to disk.
In this thread pool tutorial I will explain how thread pools work, how they are used, and how to implement a Java thread pool. Keep in mind, that Java already contains a built-in thread pool - the Java ExecutorService - so you can use a thread pool in Java without having to implement it yourself. However, once in a while you might want to implement your own thread pool - to add functionality that is not supported by the ExecutorService. Or, you may want to implement your own Java thread pool simply as a learning experience.
Thread Pool Tutorial Video
If you prefer video, I have a video version of this thread pool tutorial here: Threads Pools in Java
How a Thread Pool Works
Instead of starting a new thread for every task to execute concurrently, the task can be passed to a thread pool. As soon as the pool has any idle threads the task is assigned to one of them and executed. Internally the tasks are inserted into a Blocking Queue which the threads in the pool are dequeuing from. When a new task is inserted into the queue one of the idle threads will dequeue it successfully and execute it. The rest of the idle threads in the pool will be blocked waiting to dequeue tasks.

Thread Pool Use Cases
Thread pools are often used in multi threaded servers. Each connection arriving at the server via the network is wrapped as a task and passed on to a thread pool. The threads in the thread pool will process the requests on the connections concurrently. A later trail will get into detail about implementing multithreaded servers in Java.
Built-in Java Thread Pool
Java comes with built in thread pools in the java.util.concurrent package, so you don't have to implement your own thread pool. You can read more about it in my text on the java.util.concurrent.ExecutorService. Still it can be useful to know a bit about the implementation of a thread pool anyways.
Java Thread Pool Implementation
Here is a simple thread pool implementation. The implementation uses the standard Java BlockingQueue that comes with Java from Java 5.
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

public class ThreadPool {

    private BlockingQueue taskQueue = null;
    private List<PoolThreadRunnable> runnables = new ArrayList<>();
    private boolean isStopped = false;

    public ThreadPool(int noOfThreads, int maxNoOfTasks){
        taskQueue = new ArrayBlockingQueue(maxNoOfTasks);

        for(int i=0; i<noOfThreads; i++){
            PoolThreadRunnable poolThreadRunnable =
                    new PoolThreadRunnable(taskQueue);

            runnables.add(new PoolThreadRunnable(taskQueue));
        }
        for(PoolThreadRunnable runnable : runnables){
            new Thread(runnable).start();
        }
    }

    public synchronized void  execute(Runnable task) throws Exception{
        if(this.isStopped) throw
                new IllegalStateException("ThreadPool is stopped");

        this.taskQueue.offer(task);
    }

    public synchronized void stop(){
        this.isStopped = true;
        for(PoolThreadRunnable runnable : runnables){
            runnable.doStop();
        }
    }

    public synchronized void waitUntilAllTasksFinished() {
        while(this.taskQueue.size() > 0) {
            try {
                Thread.sleep(1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

}

Below here is the PoolThreadRunnable class which implements the Runnable interface, so it can be executed by a Java thread:
import java.util.concurrent.BlockingQueue;

public class PoolThreadRunnable implements Runnable {

    private Thread        thread    = null;
    private BlockingQueue taskQueue = null;
    private boolean       isStopped = false;

    public PoolThreadRunnable(BlockingQueue queue){
        taskQueue = queue;
    }

    public void run(){
        this.thread = Thread.currentThread();
        while(!isStopped()){
            try{
                Runnable runnable = (Runnable) taskQueue.take();
                runnable.run();
            } catch(Exception e){
                //log or otherwise report exception,
                //but keep pool thread alive.
            }
        }
    }

    public synchronized void doStop(){
        isStopped = true;
        //break pool thread out of dequeue() call.
        this.thread.interrupt();
    }

    public synchronized boolean isStopped(){
        return isStopped;
    }
}

And here is finally an example of how to use the ThreadPool above:
public class ThreadPoolMain {

    public static void main(String[] args) throws Exception {

        ThreadPool threadPool = new ThreadPool(3, 10);

        for(int i=0; i<10; i++) {

            int taskNo = i;
            threadPool.execute( () -> {
                String message =
                        Thread.currentThread().getName()
                                + ": Task " + taskNo ;
                System.out.println(message);
            });
        }

        threadPool.waitUntilAllTasksFinished();
        threadPool.stop();

    }
}

The thread pool implementation consists of two parts. A ThreadPool class which is the public interface to the thread pool, and a PoolThread class which implements the threads that execute the tasks.
To execute a task the method ThreadPool.execute(Runnable r) is called with a Runnable implementation as parameter. The Runnable is enqueued in the blocking queue internally, waiting to be dequeued.
The Runnable will be dequeued by an idle PoolThread and executed. You can see this in the PoolThread.run() method. After execution the PoolThread loops and tries to dequeue a task again, until stopped.
To stop the ThreadPool the method ThreadPool.stop() is called. The stop called is noted internally in the isStopped member. Then each thread in the pool is stopped by calling doStop() on each thread. Notice how the execute() method will throw an IllegalStateException if execute() is called after stop() has been called.
The threads will stop after finishing any task they are currently executing. Notice the this.interrupt() call in PoolThread.doStop(). This makes sure that a thread blocked in a wait() call inside the taskQueue.dequeue() call breaks out of the wait() call, and leaves the dequeue() method call with an InterruptedException thrown. This exception is caught in the PoolThread.run() method, reported, and then the isStopped variable is checked. Since isStopped is now true, the PoolThread.run() will exit and the thread dies.

## Multithreading


Source: https://www.baeldung.com/java-thread-lifecycle 

(Using Springboot) Multi-threading is similar to multi-tasking, but it enables the processing of executing multiple threads simultaneously, rather than multiple processes. CompletableFuture, which was introduced in Java 8, provides an easy way to write asynchronous, non-blocking, and multi-threaded code.

The Future interface was introduced in Java 5 to handle asynchronous computations. But, this interface did not have any methods to combine multiple asynchronous computations and handle all the possible errors. The  CompletableFuture implements Future interface, it can combine multiple asynchronous computations, handle possible errors and offers much more capabilities.

See link for examples: https://dzone.com/articles/multi-threading-in-spring-boot-using-completablefu 







	
## Concurrency

https://www.tutorialspoint.com/java_concurrency/concurrency_overview.htm

Java is a multi-threaded programming language which means we can develop multi-threaded program using Java. A multi-threaded program contains two or more parts that can run concurrently and each part can handle a different task at the same time making optimal use of the available resources specially when your computer has multiple CPUs.

By definition, multitasking is when multiple processes share common processing resources such as a CPU. Multi-threading extends the idea of multitasking into applications where you can subdivide specific operations within a single application into individual threads. Each of the threads can run in parallel. The OS divides processing time not only among different applications, but also among each thread within an application.

Multi-threading enables you to write in a way where multiple activities can proceed concurrently in the same program.

Life Cycle of a Thread
A thread goes through various stages in its life cycle. For example, a thread is born, started, runs, and then dies. The following diagram shows the complete life cycle of a thread.



Java Thread
Following are the stages of the life cycle −

New − A new thread begins its life cycle in the new state. It remains in this state until the program starts the thread. It is also referred to as a born thread.

Runnable − After a newly born thread is started, the thread becomes runnable. A thread in this state is considered to be executing its task.

Waiting − Sometimes, a thread transitions to the waiting state while the thread waits for another thread to perform a task. A thread transitions back to the runnable state only when another thread signals the waiting thread to continue executing.

Timed Waiting − A runnable thread can enter the timed waiting state for a specified interval of time. A thread in this state transitions back to the runnable state when that time interval expires or when the event it is waiting for occurs.

Terminated (Dead) − A runnable thread enters the terminated state when it completes its task or otherwise terminates.

Thread Priorities
Every Java thread has a priority that helps the operating system determine the order in which threads are scheduled.

Java thread priorities are in the range between MIN_PRIORITY (a constant of 1) and MAX_PRIORITY (a constant of 10). By default, every thread is given priority NORM_PRIORITY (a constant of 5).

Threads with higher priority are more important to a program and should be allocated processor time before lower-priority threads. However, thread priorities cannot guarantee the order in which threads execute and are very much platform dependent.

## Parallelism

https://www.geeksforgeeks.org/difference-between-concurrency-and-parallelism/

Parallelism is related to an application where  tasks are divided into smaller sub-tasks that are processed seemingly simultaneously or parallel. It is used to increase the throughput and computational speed of the system by using multiple processors. It enables single sequential CPUs to do a lot of things “seemingly” simultaneously.
Parallelism leads to overlapping of central processing units and input-output tasks in one process with the central processing unit and input-output tasks of another process. Whereas in concurrency the speed is increased by overlapping the input-output activities of one process with CPU process of another process. 

	



## Synchronous vs Asynchronous
A synchronous request blocks the client until operation completes i.e. browser is blocked and unresponsive. An asynchronous request doesn’t block the client i.e. browser is responsive. At that time, users can perform other operations also. 

Source: https://www.javatpoint.com/understanding-synchronous-vs-asynchronous
	
## Deadlocks and Livelocks
A deadlock occurs when two or more threads wait forever for a lock or resource held by another of the threads. Consequently, an application may stall or fail as the deadlocked threads cannot progress. Deadlock is a common concurrency problem in Java so we should avoid the need for acquiring multiple locks for a thread and design a Java application to avoid any potential deadlock conditions. However, if a thread does need multiple locks, we should make sure that each thread acquires the locks in the same order, to avoid any cyclic dependency in lock acquisition.
We can also use timed lock attempts, like the tryLock method in the Lock interface, to make sure that a thread does not block infinitely if it is unable to acquire a lock.
Livelock is another concurrency problem and is similar to deadlock. In livelock, two or more threads keep on transferring states between one another instead of waiting infinitely as we saw in the deadlock example. Consequently, the threads are not able to perform their respective tasks.
A great example of livelock is a messaging system where, when an exception occurs, the message consumer rolls back the transaction and puts the message back to the head of the queue. Then the same message is repeatedly read from the queue, only to cause another exception and be put back on the queue. The consumer will never pick up any other message from the queue.
To avoid a livelock, we need to look into the condition that is causing the livelock and then come up with a solution accordingly.
For example, if we have two threads that are repeatedly acquiring and releasing locks, resulting in livelock, we can design the code so that the threads retry acquiring the locks at random intervals. This will give the threads a fair chance to acquire the locks they need.
Another way to take care of the liveness problem in the messaging system example we've discussed earlier is to put failed messages in a separate queue for further processing instead of putting them back in the same queue again.
Source: https://www.baeldung.com/java-deadlock-livelock
	
## Race Conditions

1. Introduction
What is a Race Condition? | Baeldung on Computer Science

One of the most common problems in multithreaded applications is the problem of race conditions.
In this tutorial, we’ll learn what race conditions are, the ways to detect them, and the approaches to handle them.
2. Race Condition
By definition, a race condition is a condition of a program where its behavior depends on relative timing or interleaving of multiple threads or processes. One or more possible outcomes may be undesirable, resulting in a bug. We refer to this kind of behavior as nondeterministic.
Thread-safe is the term we use to describe a program, code, or data structure free of race conditions when accessed by multiple threads.
Let’s consider a simple function for performing a funds transfer between two bank accounts:
In this implementation, we thought thru the possibility to attempt to withdraw funds that are not available at the source account. Thus, we have a check for the amount available, and we expect the account balance would never go below zero. Let’s say we have accounts A and B, each having a balance of 500, and we perform two attempts to transfer 300 from A to B:

However, if these two attempts are kicked off simultaneously, in different processes or threads, we may observe some undesired behavior:

Given unpredictable thread scheduling, the order of specific steps is arbitrary. We’ve encountered a race condition due to the interleaving of our execution flows
3. Check-Then-Act
In our bank funds transfer example, we’ve observed the pattern check-then-act.
This is the most common type of race condition. It’s defined by a program flow where a potentially stale observation is used to decide what to do next. We refer to the bugs produced by this condition as Time-of-check to time-of-use or TOCTOU bugs.
TOCTOU races are often found to be the reason for security vulnerabilities on various platforms, specifically around file systems access. Attackers exploit these vulnerabilities to get privilege escalation or to perform a denial-of-service attack.
Lazy initialization is yet another example of a check-then-act patter
4. Read-Modify-Write
While the check-then-act type of race condition is indeed the most common type we may encounter in multi-threaded applications, there’s another, easier-to-grasp type. Consider the following pseudocode, which uses the regular increment operation:

 
In most languages, the regular increment operator represents three sequential operations — read, modify, and write.
Since we haven’t indicated any atomic guarantee for this execution, if more than one execution is started, we may get the very same operation interleaving we’ve seen before:

This type of condition is closely related to the data race. We’ll discuss this subtle difference below, but let’s talk about the practical aspects first.
5. Detection
A race condition is usually difficult to reproduce, debug, and eliminate. We describe the bugs introduced by race conditions as heisenbugs.
Since race conditions are tied to application semantics, there’s no general way to detect them. Multi-threaded unit tests with a focus on test result stability will help but are unlikely to provide a 100% guarantee.

## Monitor Design Pattern
One of eight concurrency patterns in Spring 5.

### Monitor object pattern
The monitor object pattern is another concurrency design pattern that helps in the execution of multi-threaded programs. It is a design pattern implemented to make sure that at a single time interval, only one method runs in a single object, and for this purpose, it synchronizes concurrent method execution.

Unlike the active object design pattern, the monitor object pattern does not have a separate thread of control. Every request received is executed in the thread of control of the client itself, and until the time the method returns, the access is blocked. At a single time interval, a single synchronized method can be executed in one monitor.

The following solutions are offered by the monitor object pattern:

The synchronization boundaries are defined by the interface of the object, and it also makes sure that a single method is active in a single object.
It must be ensured that all the objects keep a check on every method that needs synchronization and serialize them transparently without letting the client know. Operations, on the other hand, are mutually exclusive, but they are invoked like ordinary method calls. Wait and signal primitives are used for the realization of condition synchronization.
To prevent the deadlock and use the concurrency mechanisms available, other clients must be allowed to access the object when the method of the object blocks during execution.
The invariants must always hold when the thread of control is interrupted voluntarily by the method.
Let's see the following diagram, which illustrates more about the monitor object design pattern in the concurrency application:


In this preceding diagram, the client object calls the monitor object that has several synchronized methods and the monitor object associated with the monitor conditions and monitor locks. Let's explore each component of this concurrency design pattern as follows:

Monitor object: This component exposes the methods that are synchronized to the clients
Synchronized methods: The thread-safe functions that are exported by the interface of the object are implemented by these methods
Monitor conditions: This component along with the monitor lock decides whether the synchronized method should resume its processing or suspend it
The active object and the monitor object patterns are the branches of design patterns of concurrency.

Now, the other type of concurrency patterns that we will discuss are the branches of architectural patterns for concurrency.

(Source: Spring 5 Design Patterns, Dinesh Rajput, Ch. 12 Implementiing Concurrency Patterns, ISBN: 9781788299459)


# Day 4

## Intro to Spring
### Spring
Spring framework is an open source Java platform that provides comprehensive infrastructure support for developing robust Java applications very easily and very rapidly. Spring framework was initially written by Rod Johnson and was first released under the Apache 2.0 license in June 2003. 

Why Learn Spring?
Spring is the most popular application development framework for enterprise Java. Millions of developers around the world use Spring Framework to create high performing, easily testable, and reusable code.

Spring is lightweight when it comes to size and transparency. The basic version of Spring framework is around 2MB.

The core features of the Spring Framework can be used in developing any Java application, but there are extensions for building web applications on top of the Java EE platform. Spring framework makes J2EE development easier to use and promotes good programming practices by enabling a POJO-based programming model.

#### Applications
Microservices
Reactive
Cloud
Web apps
Serverless
Event Driven
Batch

#### Applications of Spring
Following is the list of few of the great benefits of using Spring Framework −

POJO Based - Spring enables developers to develop enterprise-class applications using POJOs. The benefit of using only POJOs is that you do not need an EJB container product such as an application server but you have the option of using only a robust servlet container such as Tomcat or some commercial product.

Modular - Spring is organized in a modular fashion. Even though the number of packages and classes are substantial, you have to worry only about the ones you need and ignore the rest.

Integration with existing frameworks - Spring does not reinvent the wheel. Instead it truly makes use of some of the existing technologies like several ORM frameworks, logging frameworks, JEE, Quartz and JDK timers, and other view technologies.

Testability - Testing an application written with Spring is simple because environment-dependent code is moved into this framework. Furthermore, by using JavaBeanstyle POJOs, it becomes easier to use dependency injection for injecting test data.

Web MVC - Spring's web framework is a well-designed web MVC framework, which provides a great alternative to web frameworks such as Struts or other over-engineered or less popular web frameworks.

Central Exception Handling - Spring provides a convenient API to translate technology-specific exceptions (thrown by JDBC, Hibernate, or JDO, for example) into consistent, unchecked exceptions.

Lightweight - IoC containers tend to be lightweight, especially when compared to EJB containers, for example. This is beneficial for developing and deploying applications on computers with limited memory and CPU resources.

Transaction management - Spring provides a consistent transaction management interface that can scale down to a local transaction (using a single database, for example) and scale up to global transactions (using JTA, for example).

#### Advantages
Trusted
Flexible
Productive 
Fast
Secure
Supportive

(Source: https://www.tutorialspoint.com/spring/index.htm  )


## Spring IOC Container
### Dependency Injection (DI)
The technology that Spring is most identified with is the Dependency Injection (DI) flavor of Inversion of Control. The Inversion of Control (IoC) is a general concept, and it can be expressed in many different ways. Dependency Injection is merely one concrete example of Inversion of Control.

When writing a complex Java application, application classes should be as independent as possible of other Java classes to increase the possibility of reusing these classes and to test them independently of other classes while unit testing. Dependency Injection helps in gluing these classes together and at the same time keeping them independent.

What is dependency injection exactly? Let's look at these two words separately. Here the dependency part translates into an association between two classes. For example, class A is dependent on class B. Now, let's look at the second part, injection. All this means is, class B will get injected into class A by the IoC.

Dependency injection can happen in the way of passing parameters to the constructor or by post-construction using setter methods. As Dependency Injection is the heart of Spring Framework, we will explain this concept in a separate chapter with relevant example.
### Spring - IoC Containers
The Spring container is at the core of the Spring Framework. The container will create the objects, wire them together, configure them, and manage their complete life cycle from creation till destruction. The Spring container uses DI to manage the components that make up an application. These objects are called Spring Beans, which we will discuss in the next chapter.
The container gets its instructions on what objects to instantiate, configure, and assemble by reading the configuration metadata provided. The configuration metadata can be represented either by XML, Java annotations, or Java code. The following diagram represents a high-level view of how Spring works. The Spring IoC container makes use of Java POJO classes and configuration metadata to produce a fully configured and executable system or application.

Spring provides the following two distinct types of containers.
Sr.No.
Container & Description
1
Spring BeanFactory Container
This is the simplest container providing the basic support for DI and is defined by the org.springframework.beans.factory.BeanFactory interface. The BeanFactory and related interfaces, such as BeanFactoryAware, InitializingBean, DisposableBean, are still present in Spring for the purpose of backward compatibility with a large number of third-party frameworks that integrate with Spring.
2
Spring ApplicationContext Container
This container adds more enterprise-specific functionality such as the ability to resolve textual messages from a properties file and the ability to publish application events to interested event listeners. This container is defined by the org.springframework.context.ApplicationContext interface.

The ApplicationContext container includes all functionality of the BeanFactorycontainer, so it is generally recommended over BeanFactory. BeanFactory can still be used for lightweight applications like mobile devices or applet-based applications where data volume and speed is significant.



(Source: https://www.tutorialspoint.com/spring/spring_overview.htm )


## Spring Ecosystem

https://springtutorials.com/spring-ecosystem/


The image splits the Spring Framework Ecosystem into five parts.
You will see three arrows going from left to right. The three arrows split the Projects into four parts:
1) Web layer, 2) Common layer, 3) Service layer and 4) Data layer. 
The three projects at the bottom of the page comprise the fifth part.
They are 5) Foundation projects and can span many layers.
1) Spring Projects on the Web layer
The following Spring projects help you with your front-end development.
Spring HATEOAS
Spring Mobile
Spring Web Flow
Spring Session
Spring Web Services
Spring Social
Spring for Android
Spring Security
Spring Security is at the center of all these projects for a reason.
It does not mean these projects surrounding Spring Security are dependent on it, but implies that all web layer projects can make use of Spring Security.
In the production environment, you will want to see these Spring Projects leveraging Spring Security.
I will go over these projects one by one and share few sentences on what they do. Later, I will identify how you can bring it in your project.
If you can use it with other Spring Projects or if a project pulls other external libraries, I will bring that up as well.
In my next post, You will see ALL web layer projects pull some common modules. I will provide details of Spring modules then.
For now, please note that I am skimming over these topics. The goal here is for you to be familiar with them.
Let’s start with Spring Session.
a) Spring Session allows you to handle web sessions in your application.
You shouldn’t store anything in HttpSession but if you must, then Spring Session Project can help you.
Use Spring Session with Spring Data Redis and you can store any session data into Redis datastore. This makes it short-lived, fast, and temporary. Also, it can solve your clustering problem.
Spring Session is a Web layer project. Spring Data is a Data layer project. And they work great together.
Spring Data Redis subproject will pull java Redis client – Jedis by default. It will also pull apache commons-pool as a result.
To use it in your project, you just need to set up the Redis Connection Factory. Spring Session will do all the magic.
You don’t need to write any more code here. So, it is easy to introduce or pull Spring Session out of your project with minimal effort.
b) Spring Web Services helps you build a contract-first SOAP-based web service. It also helps you consume an SOAP-based web service with Spring.
Contract-first based web service means you write WSDL first. WSDL stands for Web Services Description Language. It is the language of the SOAP web service. You need it to explain to your client what they can consume. It defines the contract.
In my opinion, a Java developer shouldn’t have to worry about description language. He should write a service in java and then a project / framework  would take care of exposing it as a web service. In my projects, I used Axis2 with Spring to achieve this.
I am not a big fan of contract-first approach to web service development. I plan to address this in a future post. For now, Let’s move on.
Spring WS pulls in Spring OXM module for converting XML into java and vice versa. This is also called Marshalling / Unmarshalling.
Spring WS code to publish a web service involves annotating your POJOs. The configuration includes generating classes from XML schema and writing logic to populate them.
It may not be easy to introduce or pull out of the Project as some code dependencies get introduced.
c) Spring Social lets facebook, LinkedIn, twitter and other users log into your site. This eliminates the need for a user to create a new account for your application.
Including it in your application involves setting up configurations based on providers. It is a standard set of code that you write once.
There is some initial setup needed to get this working. But swapping the facebook login to your home-grown login is easy. Thanks to Spring Security.
d) Spring for Android helps you build native android applications.
This is not invasive by any means. The bigger effort here is learning android SDK and getting used to Android Studio.
In my opinion, Mobile-first Javascript MVC frameworks are a much better option. They are easy to build and debug.
Spring Android team, if you are reading this, I’d love to know otherwise.
e) Spring HATEOAS helps your create REST representations that follow HATEOAS principle.
Here is another effort to explain what it means:
Your web page provides links to other pages.
With HATEOAS, your REST services can return metadata about other discoverable services or representations.
This is the premise behind semantic web. And I know one person who can explain it well: Brian Sletten.
Check out Brian Sletten’s article on HATEOAS.  Here is a video of him going over REST. If you would like to understand the R in REST, I suggest you check out this post from him as well.
Spring HATEOAS sits on top of Spring web-MVC. It has no other dependency which makes it easy to introduce or pull it out of your projects.
f) Spring Mobile helps you build mobile friendly pages. It can detect if your requests are coming from a mobile device.
You can then render pages based on this information as you see fit.
It is easy to add to your view renderer. In my case, I was using tiles to send users to appropriate pages based on the device.
So you write two sets of web pages, one that caters to mobile device audience and the other one for regular web.
I don’t know if this is a good approach. Once again, I think there is a better way in javascript MVC frameworks like Angular JS to achieve this.
AngularJS provides a responsive design. You may not need two sets of pages as a result.
It is easy to introduce Spring Mobile and pull it out if needed.
g) Spring Web Flow splits data into many screens for easy navigation.
Some of Spring Projects are frameworks. They take some time to incorporate into your project. Once they are in, they can provide for a lot of features. Once they are in, they are hard to replace as time goes by.
Spring Web Flow fits in here. If you decide to replace Spring Web Flow, you have to think about how to handle things that were a given.
It many not be easy to replace. And for a good reason.
All those hidden variables that Spring Web Flow handled for you – You may have to handle them on your own now.
h) Spring Security is at the heart of this layer. If you are writing a web application,  you will need to interact with a robot or a user at some point. Spring Security makes your application secure. It controls who can interact with your application and at what levels.
Spring Security is almost irreplaceable in my opinion.
I have heard good things about Apache Shiro but have not tried it yet. If I skip Apache Shiro for a few seconds, I can’t imagine replacing Spring Security Framework. Any custom solution just wouldn’t cut it.
The separation of concern and level of isolation Spring Security provides is excellent. Try implementing it yourself with filters and you will appreciate its power more.
Spring Security bring its own database schema. If you are not overriding the schema, You may need database team approval.
Spring Security can include Spring LDAP for authentication and/or authorization.
2) Common layer – Spring Framework Project
All these projects in different layers have one thing in common:
They all leverage Spring Framework.
A Spring Framework has 20 modules as I mentioned earlier. These twenty modules fall under six categories.
1) Spring Web
2) Spring Test
3) Spring Data Access/Integration
4) Spring AOP and Instrumentation
5) Spring Messaging
6) Spring Core Container
When I say they all leverage Spring Framework, I mean:
All Spring Projects make use of one or more of these modules.
That’s all I want to say about modules today. More to come soon.
3) Service layer Projects
In my little experience, the following projects would make great services.
This is debatable, though, but I have a reason to include them into service layer and am willing to take my chances.
Spring Integration
A file poller scenario I gave in my previous post is a good example.
If you think about it, file polling might fit into data layer as well. After all, you are dealing with data here.
But then again, You are polling which is not a true data manipulation. It is an event.
You want to capture this event on a service layer. The process is more visible that way. You can take some action based on this event now.
And these actions could mean data manipulation for sure.  Data manipulation belongs in the data layer. The event – not so much.
Spring Integration is perfect for handling event-based actions. You can plug it on top of any Spring Data layer projects.
Spring Cloud
I am new to Spring Cloud.
I was thinking Spring Cloud should be a foundation layer project at first. I will discuss foundation layer projects soon. With so many subprojects under it, I can see Spring Cloud Project as a toolkit.
And it IS a toolkit for building distributed applications. Let me explain.
Let’s say you were building a service that you would want to distribute and scale at some point. What are some of the things that you would have to take into account?
I would want the service to scale. If the calls grow, the service should handle it.
I would want discoverability. If few nodes die, the service shouldn’t die. It should know to at least reconfigure and remove the dead nodes from its network.
I should have a way to see the nodes and their status.
I would want it to be distributed.  Regardless of nodes dying, It should finish the job.
I would love for it to be testable. I want to be able to simulate all the aspects of distributed app.
I see subprojects under Spring Cloud that handle log tracing, configuration management, and security.
I see subprojects under Spring Cloud that handle discovery. I see that I can upload my service to the cloud foundry for scalability.
I see that Spring Cloud lets me write a service once that I can deploy in any infrastructure.
But I do realize that as a Developer, I would expose parts of my application to this distribution. Not the entire application.
So, I would expose my services to Spring Cloud. And I decided to add it to Service layer.
The best way to include Spring Cloud projects in your application would be via the release train.
Each release train will know to pull right dependencies for specific subprojects for you.
These dependencies are complex. These dependencies are many projects weaved together for compliance.
In maven convention, release trains are BOM – Bill of Materials.
 
This needs some explanation….
 
A POM in maven is a Project Object Model. It contains all the libraries your application needs. If you use maven in your application, this is your pom.xml.
Spring Cloud projects could have intricate dependencies. Instead of letting Spring developers meddle with versions, Spring Cloud put together a BOM.
A BOM has in it defined all the libraries and their versions that a developer will need to pull.
A project leveraging Spring Cloud would bring this BOM into dependencyManagement in its POM.
Now you could bring a Spring Cloud subproject into your application. And the BOM would take care of the versions.
First I heard of BOM was in regards to JBoss AS7 application server.
I don’t know how easy it would be to bring Spring Cloud into your projects or pull it out yet. I am still learning this one.
4) Data layer Projects
The projects in this layer deal with data handling and manipulation. Let’s discuss them one by one below.
Spring AMQP
Spring AMQP abstracts out dealing with sending and receiving messages. It provides a low-level template to interact with data. It provides a connection factory. It provides a pre-built implementation in RabbitMQ.
It provides a listener container. For this reason, It almost fell into Service layer project. I had to think at least ten times before pulling it out of Service layer.
What made my decision to keep it in Data layer? I realized that with spring, a developer deals with messages via a template. Just like when he deals with the databases with jdbcTemplate.
Note: Spring Rabbit will bring RabbitMQ and Jackson libraries with it. I like RabbitMQ. You should check it out.
Spring LDAP
Some Spring projects are libraries. They can go into your project with minimal impact to the rest of the code.
Spring LDAP is a good example.
Add Spring LDAP to your project as a library. Create a service to look up users’ roles and swap it as an implementation to do authorization. If you use Spring Security, your application won’t even notice this change.
Spring LDAP is easy to introduce in your project. It is easy to pull out as well.
Spring Data
Spring Data, like Spring Cloud, is another umbrella project with many wonderful offerings.
Think of Spring Data as a common API to do CRUD operations for different databases. It has support for all the popular SQL as well as NoSQL databases.
With Spring Data, It is possible to swap your database with minimal code changes. Especially if you don’t do anything database-specific with your code.
If you use Hibernate, you could use Spring Data JPA underneath it. You will cut down your boilerplate code to a great extent.
You won’t be writing CREATE, READ, UPDATE and DELETE (CRUD) implementations now.
You won’t be implementing ANDs or FindBy methods anymore.
What will you do with all that extra time?
If you take Spring Data out of your project, you do all the boilerplate coding.
Spring Data provides a BOM for inclusion as well.
Spring Batch
Some Projects need extra time and resource investment.
Spring Batch, like Spring Web Flow, is another example of framework project. It is a framework with lots of features. And it requires commitment.
You can use Spring Batch to do any bulk processing job. These are long running queries that you need running in the background.
Spring Batch, like Spring Security, bring its own database schema. It takes time to learn the schema. I don’t know if you want to override their schema. So you will need database team approval here.
It is not easy to replace the features Spring Batch provides.
5) Foundation Projects
Some of the Spring Projects are platforms. In the image above, you see them at the bottom of the page.
These projects don’t belong to any one layer. Rather, they serve as a foundation for other Spring Projects. Let’s discuss them below.
Spring IO Platform
I am new to Spring IO.
If you were starting your application from scratch. And if you have decided to use Spring Framework, which library would you pull first?
You will need to include just one BOM: platform-bom
You could then bring in any of the Spring Projects without worrying about their versions. Or dependencies. BOM includes all the information.
Spring IO makes it easy to bring in what you need for your application.
Spring IO Platform provides Spring Boot under its belt.
You could use Spring Boot to run the application that you built using Spring IO Platform.
You are not tied to Spring IO platform. It generates the artifacts which you can decide to edit as you see fit.
Spring Boot
It is the easiest way to build and run your application. It gives you a command line tool to build an application in shortest time frame.
The tool generates the ‘same old same old’ code you write when you start an application.
I use WordPress for hosting Spring Tutorials Blog. Spring Boot is like installing a WordPress plugin for me.
The plugin gets installed and configured with default values with a click of a button.
It cuts down your getting up and running time.
Spring Boot is a facilitator of your application. You can get started with it and later decide to not leverage it.
Spring XD
I am new to Sping XD.
Spring Cloud provides a way to build and manage distributed services.
Spring XD provides a way to build and manage big data applications. Spring XD also helps you perform big data analytics on these applications.
This implies the ability to leverage big data Hadoop or other technologies with minimal effort.
I see that Spring XD is being rebuilt on top of Spring Boot and Spring Cloud.
I am sure Spring XD will simplify weaving all aspects of big data applications. Taking it out of your project may not be the best idea.


## Dependency Injection

In software engineering, dependency injection is a technique in which an object receives other objects that it depends on, called dependencies. Typically, the receiving object is called a client and the passed-in ('injected') object is called a service. The code that passes the service to the client is called the injector. Instead of the client specifying which service it will use, the injector tells the client what service to use. The 'injection' refers to the passing of a dependency (a service) into the client that uses it.
The service is made part of the client's state.[1] Passing the service to the client, rather than allowing a client to build or find the service, is the fundamental requirement of the pattern.
The intent behind dependency injection is to achieve separation of concerns of construction and use of objects. This can increase readability and code reuse.
Dependency injection is one form of the broader technique of inversion of control. A client who wants to call some services should not have to know how to construct those services. Instead, the client delegates to external code (the injector). The client is not aware of the injector.[2] The injector passes the services, which might exist or be constructed by the injector itself, to the client. The client then uses the services.
This means the client does not need to know about the injector, how to construct the services, or even which services it is actually using. The client only needs to know the interfaces of the services, because these define how the client may use the services. This separates the responsibility of 'use' from the responsibility of 'construction'.
Types of dependency injection

There are at least three ways a client can receive a reference to an external module:[31]
Constructor injection: The dependencies are provided through a client's class constructor.
Setter injection: The client exposes a setter method that the injector uses to inject the dependency.
Interface injection: The dependency's interface provides an injector method that will inject the dependency into any client passed to it.
DI frameworks and testing frameworks can use other types of injection.[32]
Some modern testing frameworks do not even require that clients actively accept dependency injection, thus making legacy code testable. In Java, reflection can make private attributes public when testing and thus accept injections by assignment.[33]
Some attempts at Inversion of Control simply substitute one form of dependency for another. As a rule of thumb, if a programmer can look at nothing but the client code and tell what framework is being used, then the client has a hard-coded dependency on the framework.


## scopes of a bean
The Spring Framework supports the following five scopes, three of which are available only if you use a web-aware ApplicationContext.
Each scope is explained in detail with examples (about 10 pages long) on this link:
https://docs.spring.io/spring-framework/docs/3.0.0.M3/reference/html/ch04s04.html
Sr.No.
Scope & Description
1
singleton
This scopes the bean definition to a single instance per Spring IoC container (default).
2
prototype
This scopes a single bean definition to have any number of object instances.
3
request
This scopes a bean definition to an HTTP request. Only valid in the context of a web-aware Spring ApplicationContext.
4
session
This scopes a bean definition to an HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.
5
global-session
This scopes a bean definition to a global HTTP session. Only valid in the context of a web-aware Spring ApplicationContext.


## Spring bean lifecycle
Bean life cycle in Java Spring
The lifecycle of any object means when & how it is born, how it behaves throughout its life, and when & how it dies. Similarly, the bean life cycle refers to when & how the bean is instantiated, what action it performs until it lives, and when & how it is destroyed. In this article, we will discuss the life cycle of the bean. 
Bean life cycle is managed by the spring container. When we run the program then, first of all, the spring container gets started. After that, the container creates the instance of a bean as per the request, and then dependencies are injected. And finally, the bean is destroyed when the spring container is closed. Therefore, if we want to execute some code on the bean instantiation and just after closing the spring container, then we can write that code inside the custom init() method and the destroy() method.
The following image shows the process flow of the bean life cycle.  

Bean Life Cycle Process Flow


## Bean Factory vs Application Context
(Both are Spring IoC Containers)
BeanFactory loads beans on-demand, while ApplicationContext loads all beans at startup. Thus, BeanFactory is lightweight as compared to ApplicationContext.
ApplicationContext enhances BeanFactory in a more framework-oriented style and provides several features that are suitable for enterprise applications.
For instance, it provides messaging (i18n or internationalization) functionality, event publication functionality, annotation-based dependency injection, and easy integration with Spring AOP features.
Apart from this, the ApplicationContext supports almost all types of bean scopes, but the BeanFactory only supports two scopes — Singleton and Prototype. Therefore, it's always preferable to use ApplicationContext when building complex enterprise applications.
The ApplicationContext automatically registers BeanFactoryPostProcessor and BeanPostProcessor at startup. On the other hand, the BeanFactory does not register these interfaces automatically.

The ApplicationContext comes with advanced features, including several that are geared towards enterprise applications, while the BeanFactory comes with only basic features. Therefore, it's generally recommended to use the ApplicationContext, and we should use BeanFactory only when memory consumption is critical.

Source: https://www.baeldung.com/spring-beanfactory-vs-applicationcontext

## Spring Family
Spring Boot
Spring Framework
Spring Data
Spring Cloud
Spring Cloud Data Flow
Spring Security
Spring GraphQL
Spring Session
Spring Integration
Spring HATEOAS
Spring REST Docs
Spring Batch
Plus more...
(see Spring Ecosystem from previous section)

DAY 5
-------------------------------------------------------------------------
# @Autorwired
The @Autowired annotation provides more fine-grained control over where and how autowiring should be accomplished. The @Autowired annotation can be used to autowire bean on the setter method just like @Required annotation, constructor, a property or methods with arbitrary names and/or multiple arguments.

## @Autowired on Setter Methods
You can use @Autowired annotation on setter methods to get rid of the <property> element in XML configuration file. When Spring finds an @Autowired annotation used with setter methods, it tries to perform byType autowiring on the method.
	
# Sterotype Annotations in Spring
Spring has provided four very useful types of stereotype annotations. If any class or bean is annotated with one of these annotations, Spring will automatically create the object of that bean and register that bean in the Spring container. Now that bean will be available for the entire application to use and we can inject those beans in any layer of the application. These annotations, listed below, are found in the org.springframework.stereotype package.
	
# @Compontent, @Service @Repository

1. @Controller: This annotation is for the controller classes of the application and is available for the presentation layer component. 

2. @Service: This annotation is for the service classes of the application where we write the business logic.

3. @Component: This is a generic annotation which we can use to  annotate REST resource classes; they can be used anywhere in the application. 

4. @Repository: This annotation is used for the repository layer components where we can contact the database directly.
                                                                                   
Spring 2.0 introduced the first stereotype annotation named as @Repository. The @Component annotation was introduced in Spring 2.5 version. Spring stereotype annotations are the markers for any class that fulfills a role within the application. These annotations have greatly reduced the burden of developers to write the code for configuring the beans in the spring configuration document. Note: These annotations are used for concrete classes but not for interfaces. 

@Controller annotation is for the class as a Spring MVC controller. It is a meta-annotation of @Component, so beans annotated with @Controller that means Spring container will detect these annotations and loads those classes marked with this annotation and container will create those objects and fully initialized bean will be ready into the container for use. If we are using this annotation then we can use handler mapping annotation @RequestMapping to mark our methods inside the controller classes at which request what method should invoke.

@Service annotation is for service classes in our application.

@Component annotation is for when our classes do not fall into either of three categories i.e. @Controller, @Service, and DAOs.

@Repository annotation is for persistence layer components. The repository is a very suitable annotation for DAOs, thus providing extra benefits to the DAOs.

Note: The @Repository annotation is a meta-annotation of the @Component annotation with similar use and functionality. In a repository annotated class, we can write the code to contact the persistence layer which is just a database.

Enabling Component Scanning: Spring Container does not create instances for those classes which are annotated with these stereotype annotations. Therefore, we have to enable component scanning explicitly in the Spring configuration document by using < context:component-scan> tag. This way, stereotype annotations will be scanned and configured only when they are scanned by the Spring Container of the Spring framework.

<context:comonent-scan base-package="com.java.trading.service" />
<context:component-scan base-package="com.java.trading.repository" />
<context:component-scan base-package="com.java.trading.controller" />
	
Spring recommends we declare specific component-scan elements instead of using the top package for scanning.

We should always use these annotations over the concrete classes of the application; not over the interfaces.

# Java package structure with Spring 
## Separation of layers, each layer is an individual module/project
### REST API
* Packaged as war (Could be jar if you are using spring boot with embedded server. Spring boot doc clearly explains how to deploy the so-call uber jar. It is deadly simple.)
* It has rest controllers that handle request/responses
* depends on Service Module below
### Service
* Packaged as jar
* Business logic abstractions, this layer has no idea how to communicate with datasource.
* It will be autowired in rest controllers
* Depends on DAO/Repository module below
### DAO/Repository
* Packaged as jar
* Talks to data source directly, has operations commonly known as CRUD. It could be simple jdbc, JPA, or even file access.
* Depends on domain module below
### Domain
* Packaged as jar
* It has your domain models, normally POJO classes. If you are using ORM, they are ORM entities.
* It could also have DTO (Data Transfer Object), which are still under hot debates. Use it or not is your call.
* You can add more modules such as utility, third party integration, etc,.,but the above are highly recommended to have.
	
# Spring Modules
The Spring framework comprises of many modules such as core, beans, context, expression language, AOP, Aspects, Instrumentation, JDBC, ORM, OXM, JMS, Transaction, Web, Servlet, Struts etc. These modules are grouped into Test, Core Container, AOP, Aspects, Instrumentation, Data Access / Integration, Web (MVC / Remoting).
	
## Test
This layer provides support of testing with JUnit and TestNG.

## Spring Core Container
The Spring Core container contains core, beans, context and expression language (EL) modules.

## Core and Beans
These modules provide IOC and Dependency Injection features.

## Context
This module supports internationalization (I18N), EJB, JMS, Basic Remoting.

## Expression Language
It is an extension to the EL defined in JSP. It provides support to setting and getting property values, method invocation, accessing collections and indexers, named variables, logical and arithmetic operators, retrieval of objects by name etc.

## AOP, Aspects and Instrumentation
These modules support aspect oriented programming implementation where you can use Advices, Pointcuts etc. to decouple the code.

The aspects module provides support to integration with AspectJ.

The instrumentation module provides support to class instrumentation and classloader implementations.

## Data Access / Integration
This group comprises of JDBC, ORM, OXM, JMS and Transaction modules. These modules basically provide support to interact with the database.

## Web
This group comprises of Web, Web-Servlet, Web-Struts and Web-Portlet. These modules provide support to create web application.
