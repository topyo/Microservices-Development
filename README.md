# Disintegrate a Monolith Application into Microservices with Amazon Elastic Container Service, Docker, and Amazon EC2
## Introduction

Monolithic architecture worked successfully for many decades. In fact, many of the most successful and largest applications were initially developed and deployed as a monolith. Many large-scale enterprise applications of big companies are still being deployed as a monolith. But with the changing market and with the emergence of new technologies, there has been a paradigm shift in the way IT industries work. There are some serious issues with monolithic architecture which most companies are trying to address these days.

### Advantages of Monolithic Architecture
    1. Development is quite simple.
    2. Testing is very simple. Just launch the application and start end-to-end testing. We can also do test automation using Selenium without any difficulty.
    3. Deploying the monolithic application is straightforward; just copy the packaged application to the server.
    4. Scalability is simple. We just need to have a new instance of the monolithic application and ask the load balancer to distribute load to the new instance as well. However, as the monolithic application grows in size, scalability becomes a serious issue.

### Disadvantages of Monolithic Architecture

    1. Flexibility: Monolithic architecture is not flexible. We can’t use different technologies. The technology stack is decided at the start and followed throughout. Once development matures, sometimes it becomes difficult to upgrade the technology stack versions, let alone incrementally adopt a newer technology.
    2. Reliability: It's not reliable. If one feature goes down, the entire application might go down.
    3. Development speed: Development is really slow in monolithic architecture. It's difficult for new team members to understand and modify the code of a large monolithic application. Code quality declines over time. With the increasing size of the code base, the IDE is overloaded and becomes slower. The larger the application, the longer it takes to start up. All these factors have a huge impact on the developers' productivity. 
    4. Building complex applications: It's difficult to build a complex application because of the limitations in terms of technologies.
    5. Scalability: Monolithic applications are difficult to scale up once they get larger. We can create new instances of the monolith and ask the load balancer to distribute traffic to the new instances, but monolithic architecture can’t scale with an increasing load. Each copy of the application instance will access all of the data, which makes caching less effective and increases memory consumption and I/O traffic. Also, different application components have different resource requirements — one might be CPU intensive while another might memory intensive. With monolithic architecture, we cannot scale each component independently.
    6. Continuous deployment:  Continuous deployment is extremely difficult. Large monolithic applications are actually an obstacle to frequent deployments. In order to update one component, we have to redeploy the entire application.

 Due to the drawbacks of monolithic applications, microservice architecture is becoming more popular and used in modern architecture. 

 Therefore, what is microservice-based architecture?
Microservice architectural is an approach to developing a single application as a suite of small services, each running in its own process and communicating with lightweight mechanisms, usually via RESTful web services or messaging. These services are built around business capabilities and independently deployable by fully automated deployment machinery. There’s a bare minimum of centralized management of these services, which may be developed in different programming languages and use different data storage technologies. Microservices are small, independently deployable units which are cloud-enabled.

![](/Microservices.png)

Schematic Diagram of a Microservices Application Deployment


## Project Objective

In this project, we will deploy a monolithic node.js application to a Docker container, then decouple the application into microservices without any downtime. The node.js application hosts a simple message board with threads and messages between users.

## Application Architecture
We will run a simple monolithic application in a Docker container, deploy the same application as microservices, then switch traffic to the microservices without any downtime. 

![](/2.png)

**Monolithic Architecture**

The entire node.js application is run in a container as a single service and each container has the same features as all other containers. If one application feature experiences a spike in demand, the entire architecture must be scaled.

**Microservices Architecture**

Each feature of the node.js application runs as a separate service within its own container. The services can scale and be updated independently of the others.
I will be complete this project in Modules for easy comprehension for future readers. This project contains 5 Modules and you must complete each module before moving to the next!
I am sure you can't wait to get started , so Lets move to move on to Module 1

## Module One - Containerize the Monolith

What are Containers?

Containers are executable units of software in which application code is packaged, along with its libraries and dependencies, in common ways so that it can be run anywhere, whether it be on desktop, traditional IT, or the cloud.

To do this, containers take advantage of a form of operating system (OS) virtualization in which features of the OS (in the case of the Linux kernel, namely the namespaces and cgroups primitives) are leveraged to both isolate processes and control the amount of CPU, memory, and disk that those processes have access to.

Containers are small, fast, and portable because unlike a virtual machine, containers do not need include a guest OS in every instance and can, instead, simply leverage the features and resources of the host OS.

Containers first appeared decades ago with versions like FreeBSD Jails and AIX Workload Partitions, but most modern developers remember 2013 as the start of the modern container era with the introduction of Docker.

![](/4.png)

## Benefits of Containers
The primary advantage of containers, especially compared to a virtual machine, is providing a level of abstraction that makes them lightweight and portable.

**Lightweight**: Containers share the machine OS kernel, eliminating the need for a full OS instance per application and making container files small and easy on resources. Their smaller size, especially compared to virtual machines, means they can spin up quickly and better support cloud-native applications that scale horizontally.  
**Portable and platform independent**: Containers carry all their dependencies with them, meaning that software can be written once and then run without needing to be re-configured across laptops, cloud, and on-premises computing environments.
**Supports modern development and architecture**: Due to a combination of their deployment portability/consistency across platforms and their small size, containers are an ideal fit for modern development and application patterns—such as DevOps, serverless, and microservices—that are built are regular code deployments in small increments.
I**Improves utilization**: Like VMs before them, containers enable developers and operators to improve CPU and memory utilization of physical machines. Where containers go even further is that because they also enable microservice architectures, application components can be deployed and scaled more granularly, an attractive alternative to having to scale up an entire monolithic application because a single component is struggling with load.

**Speed:**  Launching a container with a new release of code can be done without significant deployment overhead. Operational speed is improved, because code built in a container on a developer’s local machine can be easily moved to a test server by simply moving the container. At build time, this container can be linked to other containers required to run the application stack.

**Dependency Control & Improved Pipeline:**  A Docker container image is a point in time capture of an application's code and dependencies. This allows an engineering organization to create a standard pipeline for the application life cycle. For example:

1. Developers build and run the container locally.
2. Continuous integration server runs the same container and executes integration tests against it to make sure it passes expectations.
3. The same container is shipped to a staging environment where its runtime behavior can be checked using load tests or manual QA.
4. The same container is shipped to production.

Being able to build, test, ship, and run the exact same container through all stages of the integration and deployment pipeline makes delivering a high quality, reliable application considerably easier.

**Density & Resource Efficiency:**  Containers facilitate enhanced resource efficiency by allowing multiple heterogeneous processes to run on a single system. Resource efficiency is a natural result of the isolation and allocation techniques that containers use. Containers can be restricted to consume certain amounts of a host's CPU and memory. By understanding what resources a container needs and what resources are available from the underlying host server, you can right-size the compute resources you use with smaller hosts or increase the density of processes running on a single large host, increasing availability and optimizing resource consumption.

**Flexibility:**  The flexibility of Docker containers is based on their portability, ease of deployment, and small size. In contrast to the installation and configuration required on a VM, packaging services inside of containers allows them to be easily moved between hosts, isolated from failure of other adjacent services, and protected from errant patches or software upgrades on the host system.

## Use cases for containers
Containers are becoming increasingly prominent, especially in cloud environments. Many organizations are even considering containers as a replacement of VMs as the general purpose compute platform for their applications and workloads. But within that very broad scope, there are key use cases where containers are especially relevant.

Microservices: Containers are small and lightweight, which makes them a good match for microservice architectures where applications are constructed of many, loosely coupled and independently deployable smaller services.
DevOps: The combination of microservices as an architecture and containers as a platform is a common foundation for many teams that embrace DevOps as the way they build, ship and run software.
Hybrid, multi-cloud: Because containers can run consistently anywhere, across laptop, on-premises and cloud environments, they are an ideal underlying architecture for hybrid cloud and multicloud scenarios where organizations find themselves operating across a mix of multiple public clouds in combination with their own data center.
Application modernizing and migration: One of the most common approaches to application modernization starts by containerizing them so that they can be migrated to the cloud. 
 

![](/3.png).

For the first module, we will  start with building a Docker container image for the monolithic node.js application and push it to 
 Container Registry (Amazon ECR) and in the next few steps, we will use **Docker**, **Github**, **Amazon Elastic Container Service (Amazon ECS)**, and **Amazon ECR** to deploy code into containers. 

**Module 1 Prerequsite**
To complete module 1, the prerequisites are 
1. *** Having An AWS account:** If you don't already have an account with AWS, you can [sign up here](https://portal.aws.amazon.com/gp/aws/developer/registration/index.html). For all the exercises in this project we will be utilizing the  ****[AWS Free Tier](https://aws.amazon.com/free/). **Note:** Some of the services may require that an AWS account should be active for more than 12 hours. If you experience difficulty with any services and have a newly created account, please wait a few hours and try again.

![](/AWS%20.png)

2. **Install Docker:** We will use Docker to build the image files that will run in the containers. Docker is an open source project that can be download using  [for Mac](https://docs.docker.com/docker-for-mac/install/) or [for Windows](https://docs.docker.com/docker-for-windows/install/) 
![](/docker.png)


Also, the Docker installation package available in the official Ubuntu repository can also be used although it may not be the latest version. To ensure we get the latest version, we’ll install Docker from the official Docker repository, add a new package source, add the GPG key from Docker to ensure the downloads are valid, and then install the package.
I will be installing Docker using some commands on my terminal. You can use the command  or use the download method. 
First, I updated existing list of packages with the command:

```
$ sudo apt update

```

Next,  I installed a few prerequisite packages which let `apt` use packages over HTTPS:

```
$ sudo apt install apt-transport-https ca-certificates curl software-properties-common

```

Then I added the GPG key for the official Docker repository to the system:

```
$ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

```
Also, I added the Docker repository to APT sources using :

```
$ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntufocal stable"

```

This will also update the package database with the Docker packages from the newly added repo.

To ensure I install the Docker repo instead of the default Ubuntu repo I use the code :

```
$ apt-cache policy docker-ce

```

 
Output of apt-cache policy docker-ce

```
docker-ce:
  Installed: (none)
  Candidate: 5:20.10.12~3-0~ubuntu-focal
  Version table:
     5:20.10.12~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.11~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.10~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.8~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.7~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.6~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.5~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.4~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.3~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.2~3-0~ubuntu-focal 500

```
I got the above output. You will also see an output like this, although the version number for Docker may be different:

Notice that `docker-ce` is not installed, but the candidate for installation is from the Docker repository for Ubuntu 20.04 (`focal`).

Finally, to install Docker, I use the command :

```
$ sudo apt install docker-ce

```

Docker is now installed, the daemon started, and the process enabled to start on boot. To check that it’s running I used the command:

```
$ sudo systemctl status docker

```

The output should be similar to the following, showing that the service is active and running:

```

● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset: enabled)
     Active: active (running) since Sat 2022-03-05 16:23:06 AST; 12s ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 16183 (dockerd)
      Tasks: 13
     Memory: 29.5M
     CGroup: /system.slice/docker.service
             └─16183 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/containerd.sock

```
3. After Docker is installed, I can verify if it is running by entering **docker --version*** in the terminal. The version number should display like :
```Docker version 20.10.12, build e91ed57```

Now that the prequsite is sorted out we can now proceed with the steps required to containerize the Monolith. 

**Step 1** We begin by Installing the AWS CLI

    - We will use the AWS Command Line Interface (AWS CLI) to push the images to Amazon ECR. You can learn about and download AWS CLI [here](http://docs.aws.amazon.com/cli/latest/userguide/installing.html). I will provide some images on how I completed this step, you can follow along to get yours installed

***Getting started with the AWS CLI**

This section provides the information about how to get started with version 2 of the AWS Command Line Interface (AWS CLI).

To access AWS services with the AWS CLI, you need an AWS account, IAM credentials, and an IAM access key pair. When running AWS CLI commands, the AWS CLI needs to have access to those AWS credentials.

To increase the security of your AWS account, AWS recommendS that you do not use your root account credentials. You should create an IAM user to provide access credentials to the tasks you'll be running in AWS.
##Step 1: Sign up to AWS
If you do not have an AWS account, complete the following steps to create one.

To sign up for an AWS account

Open https://portal.aws.amazon.com/billing/signup.

![](/AWS1.png)

Follow the online instructions.

Part of the sign-up procedure involves receiving a phone call and entering a verification code on the phone keypad. Since I already have an AWS account, I moved to step 2

Step 2: Create an IAM user account
To create an administrator user for yourself and add the user to an administrators group (console)

1. Sign in to the IAM console as the account owner by choosing Root user and entering your AWS account email address. On the next page, enter your password.

2. In the navigation pane, choose Users and then choose Add user.

3. For User name, enter Administrator.

4. Select the check box next to AWS Management Console access. Then select Custom password, and then enter your new password in the text box.
5.  (Optional) By default, AWS requires the new user to create a new password when first signing in. You can clear the check box next to User must create a new password at next sign-in to allow the new user to reset their password after they sign in.

6. Choose Next: Permissions.

7. Under Set permissions, choose Add user to group.

8. Choose Create group.

9. In the Create group dialog box, for Group name enter Administrators.

10. Choose Filter policies, and then select AWS managed - job function to filter the table contents.

11. In the policy list, select the check box for AdministratorAccess. Then choose Create group.

Note
You must activate IAM user and role access to Billing before you can use the AdministratorAccess permissions to access the AWS Billing and Cost Management console. To do this, follow the instructions in step 1 of the tutorial about delegating access to the billing console.

12. Back in the list of groups, select the check box for your new group. Choose Refresh if necessary to see the group in the list.

13. Choose Next: Tags.

14. (ptional) Add metadata to the user by attaching tags as key-value pairs. For more information about using tags in IAM, see Tagging IAM entities in the IAM User Guide.

15. Choose Next: Review to see the list of group memberships to be added to the new user. When you are ready to proceed, choose Create user.


### Step 3: Create an access key ID and secret access key
For CLI access, you need an access key ID and secret access key. Use IAM user access keys instead of AWS account root user access keys. IAM lets you securely control access to AWS services and resources in your AWS account. For more information about creating access keys, see Understanding and getting your security credentials in the AWS General Reference.

Access keys consist of an access key ID and secret access key, which are used to sign programmatic requests that you make to AWS. If you don't have access keys, you can create them from the AWS Management Console. As a best practice, do not use the AWS account root user access keys for any task where it's not required. Instead, create a new administrator IAM user with access keys for yourself.

The only time that you can view or download the secret access key is when you create the keys. You cannot recover them later. However, you can create new access keys at any time. You must also have permissions to perform the required IAM actions. For more information, see Permissions required to access IAM resources in the IAM User Guide.

To create access keys for an IAM user

1. Sign in to the AWS Management Console and open the IAM console at https://console.aws.amazon.com/iam/.

2. In the navigation pane, choose Users.

3. Choose the name of the user whose access keys you want to create, and then choose the Security credentials tab.

4. In the Access keys section, choose Create access key.

5. To view the new access key pair, choose Show. You will not have access to the secret access key again after this dialog box closes. Your credentials will look something like this:

Access key ID: AKIAIOSFODNN7EXAMPLE

Secret access key: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY

6. To download the key pair, choose Download .csv file. Store the keys in a secure location. You will not have access to the secret access key again after this dialog box closes.

Keep the keys confidential in order to protect your AWS account and never email them. Do not share them outside your organization, even if an inquiry appears to come from AWS or Amazon.com. No one who legitimately represents Amazon will ever ask you for your secret key.

7. After you download the .csv file, choose Close. When you create an access key, the key pair is active by default, and you can use the pair right away.

## Installing or updating the latest version of the AWS CLI

To install the AWS CLI, you can either download and install on your local PC or you can use some commands on your linux terminal to get it installed. For details on download and install AWS CLI <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html">Click here!</a>
I will be using my local PC terminal to install AWS and below are the images and steps I took. Feel free to follow along
First,I  downloaded the installer using the curl command – The -o option specifies the file name that the downloaded package is written to. The options on the following example command write the downloaded file to the current directory with the local name awscliv2.zip.

![](/AWS3.png)

Then,  I unzipped the installer using the command:

$ unzip awscliv2.zip

If your Linux distribution doesn't have a built-in unzip command, use an equivalent to unzip it. The above command unzips the package and creates a directory named aws under the current directory.

![](/AWS4.png)

Next, I ran the install program. The installation command uses a file named install in the newly unzipped aws directory. By default, the files are all installed to /usr/local/aws-cli, and a symbolic link is created in /usr/local/bin. The command includes sudo to grant write permissions to those directories.

$ sudo ./aws/install

You can install without sudo if you specify directories that you already have write permissions to. Use the following instructions for the install command to specify the installation location:

Ensure that the paths you provide to the -i and -b parameters contain no volume name or directory names that contain any space characters or other white space characters. If there is a space, the installation fails.

--install-dir or -i – This option specifies the directory to copy all of the files to.

The default value is /usr/local/aws-cli.

--bin-dir or -b – This option specifies that the main aws program in the install directory is symbolically linked to the file aws in the specified path. You must have write permissions to the specified directory. Creating a symlink to a directory that is already in your path eliminates the need to add the install directory to the user's $PATH variable.

The default value is /usr/local/bin.

$ ./aws/install -i /usr/local/aws-cli -b /usr/local/bin

Lastly, I confirmed the installation with the following command.

$ aws --version

![](/AWS5.png)

**Note**
If you already have AWS CLI installed, run the following command in the terminal to ensure it is updated to the latest version: 

```bash
*pip install awscli --upgrade --user*
```

## Note: If you have never used AWS CLI before, you may need to s<p><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html">configure your credentials here !</a></p>

Since I have not configured AWS CLI before for the user I created earlier, I configured their credentials on linux terminal using the command 

![](/AWS6.png)
``
$ aws configure
AWS Access Key ID [None]: AKIAIOSFODNN7EXAMPLE
AWS Secret Access Key [None]: wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
Default region name [None]: us-west-2
Default output format [None]: json
``

## STEP 2 :

a) Have a text editor: If you don't already have a text editor for coding, install one to your local environment.You can use <p><a href="https://atom.io/">Atom</a></p>
Atom is a simple, open-source text editor from GitHub that is popular with developers.
or 
<p><a href="https://code.visualstudio.com/">Visual Studio Code</a></p> 
Visual Studio Code (VS code) is a lightweight but powerful source code editor which runs on your desktop and is available for Windows, macOS and Linux. It comes with built-in support for JavaScript, TypeScript and Node.js and has a rich ecosystem of extensions for other languages (such as C++, C#, Java, Python, PHP, Go) and runtimes (such as .NET and Unity). Begin your journey with VS Code with these introductory videos.

![](/vs.png)

For this project, I will be using the VS Code as my editor you are free to use the suggested above any text editor of your choice.

b)  **Download the code from GitHub:** Navigate to [https://github.com/awslabs/amazon-ecs-nodejs-microservices](https://github.com/awslabs/amazon-ecs-nodejs-microservices) and select **Clone or Download** to download the GitHub repository to your local environment. You can also use [GitHub Desktop](https://desktop.github.com/) or [Git](https://git-scm.com/) to clone the repository on your local terminal.

I cloned the repository to my terminal using the command:

![](/Git1.png)

and then navigated to Vscode (editor). 

![](/Git2.png)

On the editor I selected ***Open New Folder***, you can select Add Project for your project. Next I selected the folder I saved the repository.

![](/Git3.png)

On selecting the folder, the below showed on the Vscode that I can now work on

![](/Git4.png)

 We can see  that the cloned folders contains information about infrastructure and services. Infrastructure holds the AWS CloudFormation infrastructure configuration code that we will use in the next step. Services contains the code that forms the node.js application.You can take a few minutes to review the files and familiarize yourself with the different aspects of the application, including the database db.json, the server server.js, package.json, and the application Dockerfile.

![](/Git5.png)


## Step 3a : Create the repository/ Provision Repository:
To create a repository we begin by 
a.  Navigate to the <p><a href=
"https://console.aws.amazon.com/ecs/home?#/repositories">Amazon ECR console</a></p>

![](/AWS7.png)

On the **Repositories** page, select **Create Repository**.

- On the Create repository page, under the General settings , enter the *api* as the name of repository.  **Note:** Under **Tag immutability**, leave the default settings.

![](/AWS8.png)

![](/AWS9.png)

After the repository is created, you will get a confirmation message

Mine looks like this 

![](/AWS9.png)


## Step 3b: Authenticate the Docker log
Before we authenticate the docker log, we need to navigate to the repository we earlier cloned.
i.e Open your terminal, and set your path to the 2-containerized/services/api section of the GitHub code in the directory you have it cloned or downloaded it into: ~/amazon-ecs-nodejs-microservices/2-containerized/services/api.
I did Mine like this

![](/AWS11.png)

After navigating to the api file, we can authenticate the docker log . To complete this step. we use the command 

![](/AWS12.png)

### Step 3c :Build the Docker Image

On the terminal on your local PC, run docker build -t api. command. NOTE :The period (.) after api is important here.

``docker build -t api .``

![](/AWS13.png)
![](/AWS14.png)

### Step 3d : Tag the Image

After the build compeletes, tag the image so you can push it to the repository using : docker tag api:latest [account-id].dkr.ecr.[region].amazonaws.com/api:latest

E.g docker tag api:latest 853242329412.dkr.ecr.ca-central-1.amazonaws.com/api:latest or docker tag api:latest 85324329412.dkr.ecr.ca-central-1.amazonaws.com/api:v1 

*** Pro tip: The :v1 represents the image build version. Every time you build the image, you should increment this version number. If you were using a script, you could use an automated number, such as a time stamp to tag the image. This is a best practice that allows you to easily revert to a previous container image build in the future ***


### Step 3e: Push the image to ECR
Run docker push to push your image to ECR
docker push [account-id].dkr.ecr.[region].amazonaws.com/api:latest
or use this command (see pro tip above)
docker push [account-id].dkr.ecr.[region].amazonaws.com/api:v1  ()
 **Note:** replace the [account-ID] and [region] placeholders with your specific information.
If you navigate to your Amazon ECR repository, you should see your image tagged *v1*.
![](/AWS15.png)
Now that my image is stored in the respository, it can be pulled back down wherever I need to run it, including Amazon Elastic Container Service.

![]](/AWS16.png)
![]](/AWS17.png)

### Module 2: Deploy the Monolith

In this module, we will use the Amazon Container Service (Amazon ECS) to instantiate a managed cluster of EC2 compute instances and deploy our image as a container running on the cluster. 

## What is Amazon Elastic Container Service?

 Container Service (Amazon ECS) is a highly scalable, high performance container management service that supports Docker containers and allows you to easily run applications on a managed cluster of Amazon EC2 instances. With simple API calls, you can launch and stop Docker-enabled applications, query the complete state of your cluster, and access many familiar features like security groups, Elastic Load Balancing, EBS volumes, and IAM roles. You can use Amazon ECS to schedule the placement of containers across your cluster based on your resource needs and availability requirements. You can also integrate your own scheduler or third-party schedulers to meet business or application specific requirements.
There is no additional charge for Amazon ECS. You pay for the AWS resources (for example, EC2 instances or EBS volumes) you create to store and run your application.

The AWS services we will be utilizing for module 2 are

<p><a href="https://aws.amazon.com/ecs/">Amazon Elastic Container Service</a></p>

<p><a href="https://aws.amazon.com/ecr/">AWS Container Registry</a></p>
<p><a href="https://aws.amzon.com/cloudformation/">AWS CloudFormation</a></p>
<p><a href="https://aws.amazon.com/elasticloadbalancing/applicationloadbalancer/">Elastic Load Balancing</a></p>

Lets look at the architecture overview before we move on 

![](/m1.png)

We deploy the monolith by following the steps below 

## Step 1. Navigate to the AWS CloudFormation console and select ***Create stack***

![](/2.1.png)

a. Select Upload a template file and choose the ecs.yml file from the GitHub project at amazon-ecs-nodejs-microservice/2-containerized/infrastructure/ecs.yml then select Next.
***Note that the GitHub project at amazon-ecs-nodejs-microservice/2-containerized/infrastructure/ecs.yml was downloaded/ cloned ealier in Module 1
![](/2.2.png)

b. For the stack name, enter *BreakTheMonolith-Demo*.(Please ensure you type the name and not copy&paste) and verify that the other parameters have the following values:
    1. Desired Capacity = *2*
    2. InstanceType = *t2.micro*
    3. MaxSize = *2*
   
    ![](/2.3.png)

c. Select **Next***
![](/2.4.png)
d. On the **Configure stack options** page, we will keep the default options and scroll down and select **Next**.

![](/2.5.png)

e. On the **Review BreakTheMonolith-Demo** page scroll to the bottom of the page, acknowledge the **Capabilities** statement by selecting the checkbox, and select **Create stack**.
![](/2.7.png)
![](/2.6.png)
f.You will see the stack with the status CREATE_IN_PROGRESS. You can select the refresh button at the top right of the screen to check the progress. This process typically takes less than 5 minutes.
![](/2.8.png)

**NOTE:** Optionally, you can use the AWS Command Line Interface (AWS CLI) to deploy AWS CloudFormation stacks. Run the following code on the terminal from the folder **amazon-ecs-nodejs-microservices/3-microservices** and replace *[region]* with your AWS Region.

```bash
$ aws cloudformation deploy \
   --template-file infrastructure/ecs.yml \
   --region [region] \
   --stack-name BreakTheMonolith-Demo \
   --capabilities CAPABILITY_NAMED_IAM
```
## Step 2. **Check your Cluster is Running**
 Navigate to the [](https://console.aws.amazon.com/ecs/home?).Your cluster should appear in the list.Mine is shown below
![](/2A.png)

Select the cluster BreakTheMonolith-Demo, then select the Tasks tab to verify that there are no tasks running.
![](/2B.png)
Select the ECS Instances tab to verify there are two Amazon EC2 instances created by the AWS CloudFormation template.⚐ Note: If you receive a message that the ECS agent is outdated, select Learn more for instructions to update the ECS agent.
![](/2C.png)

Task definitions specify how Amazon ECS deploys the application containers across the cluster.

- From the **Amazon ECS** left navigation menu, select **Task Definitions**.
![](/2d.png)
- Select **Create new Task Definition**.
![](/2e.png)
- On the **Select launch type compatibility** page, select the **EC2** option then select **Next step**.
![](/2f.png)

- On the **Configure task and container definitions** page, do the following:
    - In the **Task Definition Name** field, enter *api*.
    - Scroll down to **Container Definitions** and select **Add container**.
    - In the **Add container** window:
        - Parameters that are not defined can be either left blank or with the default settings.
        - In the **Container name** field, enter *api*.
        - In the **Image** field, enter *[account-ID].dkr.ecr.[region].amazonaws.com/api:v1*Replace *[account-ID]* and *[region]* with your specific information. Ensure the tag *v1* matches the value you used in Module 1 to tag and push the image. This is the URL of your ECR repository image that was created in the previous module.
        - In the **Memory Limits** field, verify **Hard limit** is selected and enter *256* as the value.
        - Under **Port mappings**, Host port = *0* and Container port = *3000*.

![](/2g.png)


        - Scroll to **ENVIRONMENT**, CPU units = *256*.
- Select **Add**.
![](/2h.png)
You will return to the **Confi85324329412page and select **Create**.
![](/2j.png)
![](/2k.png)

The  Task Definition is listed in the console.
![](/2l.png)

## Step 3 Configuring the Application Load Balancer: Target Group

Elastic Load Balancing automatically distributes your incoming traffic across multiple targets, such as EC2 instances, containers, and IP addresses, in one or more Availability Zones. It monitors the health of its registered targets, and routes traffic only to the healthy targets. Elastic Load Balancing scales your load balancer as your incoming traffic changes over time. It can automatically scale to the vast majority of workloads.Elastic Load Balancing supports the following load balancers: Application Load Balancers, Network Load Balancers, Gateway Load Balancers, and Classic Load Balancers. You can select the type of load balancer that best suits your needs. 

## Application Load Balancer components
A load balancer serves as the single point of contact for clients. The load balancer distributes incoming application traffic across multiple targets, such as EC2 instances, in multiple Availability Zones. This increases the availability of your application. You add one or more listeners to your load balancer.

A listener checks for connection requests from clients, using the protocol and port that you configure. The rules

 that you define for a listener determine how the load balancer routes requests to its registered targets. Each rule consists of a priority, one or more actions, and one or more conditions. When the conditions for a rule are met, then its actions are performed. You must define a default rule for each listener, and you can optionally define additional rules

.

Each target group routes requests to one or more registered targets, such as EC2 instances, using the protocol and port number that you specify. You can register a target with multiple target groups. You can configure health checks on a per target group basis. Health checks are performed on all targets registered to a target group that is specified in a listener rule for your load balancer.


The following diagram illustrates the basic components. Notice that each listener contains a default rule, and one listener contains another rule that routes requests to a different target group. One target is registered with two target groups.
![](/load.png)

## Application Load Balancer overview

An Application Load Balancer functions at the application layer, the seventh layer of the Open Systems Interconnection (OSI) model. After the load balancer receives a request, it evaluates the listener rules

 in priority order to determine which rule to apply, and then selects a target from the target group for the rule action. You can configure listener rules

 to route requests to different target groups based on the content of the application traffic. Routing is performed independently for each target group, even when a target is registered with multiple target groups. You can configure the routing algorithm used at the target group level. The default routing algorithm is round robin; alternatively, you can specify the least outstanding requests routing algorithm.
You can add and remove targets from your load balancer as your needs change, without disrupting the overall flow of requests to your application. Elastic Load Balancing scales your load balancer as traffic to your application changes over time. Elastic Load Balancing can scale to the vast majority of workloads automatically.

Before we configure the application load balancer, we will 

**Check VPC Name:** If this is not your first time using this AWS account, you may have multiple VPCs. It is important to configure your Target Group with the correct VPC. Then, Navigate to the <p><a href="https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:" >Load Balancer section of the EC2 Console</a><p>

- Locate the Load Balancer 
Load balancer: Break-ECSAL-1XRL5U02HPG1S

![](/3a.png)

- Select the checkbox next to Break-ECSAL-1XRL5U02HPG1S to see the Load Balancer details.
![](/3b.png)

- In the **Description** tab, locate the **VPC** attribute (in this format: vpc-0d78c582441842195). **Note:** You will need the VPC attribute in the next step when you configure the ALB target group.
![](/3c.png]

## Step 4: **Configure the ALB Target Group**

- Navigate to the [Target Group section of the<p><a href="https://console.aws.amazon.com/ec2/v2/home?#TargetGroups:">EC2 Console</a></p>

- Select **Create target group**

![](/3e.png]

- Configure the following Target Group parameters (for the parameters not listed below, keep the default values):
    - For the **Target group name**, enter *api*.
    - For the **Protocol**, select **HTTP**.
    - For the **Port**, enter *80*.
    - For the VPC, select the value that matches the one from the Load Balancer description. .
        
       **Note** This is most likely NOT your default VPC

        ![](/3f.png)
        
    - Access the **Advanced health check settings** and edit the following parameters as needed:
        - For **Healthy threshold**, enter *2*.
        - For **Unhealthy threshold**, enter *2*.
        - For **Timeout**, enter *5*.
        - For **Interval**, enter *6*.

![](/3g.png)


- Select **Create target group**.
![](/3h.png)
![](/3i.png)


Step5 : **Add a Listener to the ALB**
A listener checks for connection requests from clients using the protocol and port configured by an organization using rules

 that determine how ALB routes requests to registered targets.
The ALB [listener](http://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html) checks for incoming connection requests to the ALB.

To add a listener to the ALB, Navigate to the [Load Balancer section of the EC2 Console](https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:).
- Select the checkbox next to to see the Load Balancer details.
- Select the **Listeners** tab.
![](/3j.png)
- Select **Add listener** and edit the following parameters as needed:
    - For **Protocol:port**, select **HTTP** and enter *80*.
    - For **Default action(s)**, select **Forward to** and in the **Target group** field, enter *api*.
- Select **Add**.
![](/3k.png)
![](/3l.png)

Step 6: Deploy the monolith as a service into the cluster.

- Navigate to the <p><a href="https://console.aws.amazon.com/ecs/home?">Amazon ECS console</a></p> and select **Clusters** from the left menu bar.
- Select the cluster **BreakTheMonolith-DemoXXXXX**, select the **Services** tab then select **Create**.
![](/3m.png)

- On the **Configure service** page, edit the following parameters (and keep the default values for parameters not listed below):
    - For the **Launch type**, select **EC2**.
    - For the **Service name**, enter *api*.
    - For the **Number of tasks**, enter *1*.
    - Select **Next step**

    ![](/3n.png)

- On the **ConfBreakad balancer name**.
    - For the **Service IAM role**, select BreakTheMonolith-Demo-ECSServiceRole.
    - For the **Load balancer name**, verify the below is selected

    ![](/load2.png)

- In the **Container to load balance** section, select **Add to load balancer**.Additional information labeled **api:3000** is shown, Click the **api:300**
- In the **api:3000** section, do the following:
    - For the **Production listener port** field, select **80:HTTP**.
    - For the **Target group name**, select your group: **api**.
    - Select **Next step**.

![](/3o.png)

- On the **Set Auto Scaling** page, leave the default setting and select **Next step**.
![](/3p.png)
- On the **Review** page, review the settings then select **Create Service**.
![](/3q.png)
- After the service has been created, select **View Service**.
![](/3r.png)
![](/3r1.png)

Nice work! We now have a running service. It may take a minute for the container to register as healthy and begin receiving traffic. please validate the deployment by checking if the service is available from the internet and pinging it.

**To Find your Service URL:**

- Navigate to the [Load Balancers](https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:) section of the EC2 Console.
- Select your load balancer
- In the **Description** tab, copy the DNS name and paste into a new browser tab or window.
- You should see the message **Ready to receive requests**.

![](/3s.png)


**See Each Part of the Service:** The node.js application routes traffic to each worker based on the URL. To see a worker, simply add the worker name *api/[worker-name]* to the end of the DNS Name as follows:

- http://*[DNS name]*/api/users
![](/users.png)
![](/apiu.png)


- http://*[DNS name]*/api/threads
![](/thread2.png)
![](thread.png)


- http://*[DNS name]*/api/posts

![](post.png)

You can also add a record number at the end of the URL to drill down to a particular record. For example: *http://[DNS name]/api/posts/1* or *http://[DNS name]/api/users/2*


## Module Three - Break the Monolith

In this module, we will break the node.js application into several interconnected services and push each service's image to an Amazon Elastic Container Registry (Amazon ECR) repository. 

## Architecture Overview

The final application architecture uses Amazon Elastic Container Service (Amazon ECS) and the Application Load Balancer (ALB).

![](/break.png)

**a. Client**The client makes traffic requests over port 80.

**b. Load Balancer** The ALB routes external traffic to the correct service. The ALB inspects the client request and uses the routing rules

 to direct the request to an instance and port for the target group matching the rule.

**c. Target Groups** Each service has a target group that keeps track of the instances and ports of each container running for that service.

**d. Microservices** Amazon ECS deploys each service into a container across an EC2 cluster. Each container only handles a single feature
To complete this module we will be using 
 <p><a href="https://aws.amazon.com/ecr/">Amazon Elastic Container Registry</a></p>
Now lets get started!Similar to ealier completed modules, we will break the monolith in steps. In the previous two modules, we deployed the application as a monolith using a single service and a single container image repository. Now to deploy the application as three microservices, we will need to provision three repositories (one for each service) in Amazon ECR.

The three services are:

1. users
2. threads
3. posts

a) Create the three repositories by repeating the following steps for each service:

- Navigate to <p><a href="(https://console.aws.amazon.com/ecs/home?#/repositories)">Amazon ECR console</a><p>

- Select **Create repository**

- In the **Create repository** page, **Repository name** field, create a repository for the service (posts, threads, or users).
- **Note:** For the **Tag immuntability** options, keep the default settings.



You should have four repositories in Amazon ECR. Record the repository information for each microservice that you created. Mine is 
![](b1.png)


This information will be needed in an upcoming step. The information you need is in the following format:*[account-id].dkr.ecr.[region].amazonaws.com/[service-name]*


You will need access to Docker to build and push the images for each service. If you are working on this project at different points in time, you may have been logged out of Docker. If this is the case, take the following steps to log into Docker again.

 Run this commmand on your terminal 

 $(aws ecr get-login --no-include-email --region [your-region])Replace [your-region], for example: $(aws ecr get-login --no-include-email --region us-west-2)
or
$ aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin [account id]].dkr.ecr.[region].amazonaws.com

If the authentication was successful, you will receive the confirmation message: **Login Succeeded**.

In the project folder **amazon-ecs-nodejs-microservices/3-microservices/services**, you will have folders with files for each service. Notice how each microservice is essentially a clone of the previous monolithic service.

You can see how each service is now specialized by comparing the file **db.json** in each service and in the monolithic api service. Previously posts, threads, and users were all stored in a single database file. Now, each is stored in the database file for its respective service.
Next navigate into 3-microservices/services file and set your path to 
*~/amazon-ecs-nodejs-microservices/3-microservices/services*
I used the command 

```$ cd ~/amazon-ecs-nodejs-microservices/3-microservices/services ```




b) **Build and Tag Each Image**

- On the terminal, run  the command 
*docker build -t [service-name] ./[service-name]
*Replace the *[service-name]*, for example: 
```
$ sudo docker build -t posts ./ posts```

![](post2.png)

- After the build completes,  we tag the image so we  can push it to the repository. We use the command 
$ sudo docker tag [service name]:latest [account-ID].dkr.ecr.[region].amazonaws.com/[service-name]:v1
For example Mine is 

Example: $ sudo docker tag posts:latest 853242329412.dkr.ecr.us-east-1 amazonaws.com/posts:v1
Finally we push the image  using the command 
$ sudo docker push [account-id].dkr.ecr.[region].amazonaws.com/[service-name]:v1

Mine is 
Example: $ sudo docker push 853242329412.dkr.ecr.us-east-1.amazonaws.com/threads:v1
$ sudo docker push 853242329412.dkr.ecr.us-east-1.amazonaws.com/posts:v1

If you navigate to your ECR repository, you should see your images tagged with v1.

Repeat these steps for each microservice image.

**NOTE:** Be sure to build and tag all three images.

## Module Four - Deploy Microservices

In this module, We will deploy the node.js application as a set of interconnected services behind an Application Load Balancer (ALB). Also, we will use the ALB to seamlessly shift traffic from the monolith to the microservices. 

## Architecture Overview

This is the process that we will follow to deploy the microservices and safely transition the application's traffic away from the monolith.

![](/arc.png)

1. **Switch the Traffic** This is the starting configuration. The monolithic node.js app running in a container on Amazon ECS.
2. **Start Microservices** Using the three container images you built and pushed to Amazon ECR in the previous module, you will start up three microservices on your existing Amazon ECS cluster.
3. **Configure the Target Groups** Like in Module 2, you will add a target group for each service and update the ALB Rules to connect the new microservices.
4. **Shut Down the Monolith** By changing one rule in the ALB, you will start routing traffic to the running microservices. After traffic reroute has been verified, shut down the monolith.
To complete this module we will be using the ffollowing AWS services 


<p><a href="(https://aws.amazon.com/ecs/)">Amazon Elastic Container Service</a></p>
<p><a href="(https://aws.amazon.com/ecr/)">Amazon Elastic Container Registry</a></p>

<p><a href="(https://aws.amazon.com/cloudformation/)">AWS CloudFormation</a></p>
<p><a href="(https://aws.amazon.com/elasticloadbalancing/applicationloadbalancer/)">Elastic Load Balancing</a></p>

Like other modules, we will complete this module as well in steps. We will deploy three new services to the cluster that we launched in Module 2. Similarto module 2, we will write Task Definitions for each of the service.

**NOTE**: It is possible to add multiple containers to a single task definition. This means you could run all three microservices as different containers from a single service. However, this approach is still monolithic since each container would need to scale linearly with the service. Our ultimate goal is to have three independent services. Each service requires its own task definition running a container with the image for that respective service. You can either create these task definitions from the Amazon ECS console, or speed things up by writing them as JSON. To write the task definition as a JSON file, follow these steps:

1. From <p><a href="(https://console.aws.amazon.com/ecs/home)">Amazon Container Service console</a></p>

under **Amazon ECS**, select **Task definitions**.
2. In the **Task Definitions** page, select the **Create new Task Definition** button.
3. In the **Select launch type compatibility** page, select the **EC2** option and then select **Next step**.
4. In the Configure task and container definitions page, scroll to the **Volumes** section and select the **Configure via JSON** button.
5. Copy and paste the following code snippet into the JSON field, replacing the existing code.Remember to replace the [service-name], [account-ID], [region], and [tag] placeholders.

**Note:** The following parameters are used for the task definition:

{
    "containerDefinitions": [
        {
            "name": "[service-name]",
            "image": "[account-id].dkr.ecr.[region].amazonaws.com/[service-name]:[tag]",
            "memoryReservation": "256",
            "cpu": "256",
            "essential": true,
            "portMappings": [
                {
                    "hostPort": "0",
                    "containerPort": "3000",
                    "protocol": "tcp"
                }
            ]
        }
    ],
    "volumes": [],
    "networkMode": "bridge",
    "placementConstraints": [],
    "family": "[service-name]"
}

Repeat the steps above and to create a task definition for each service:

posts
threads

![](thread3.png)
users

![](all.png)

As we did in Module 2, we will configure a target group for each service (posts, threads, and users). A target group allows traffic to correctly reach a specified service. we will configure the target groups using AWS CLI. However, before proceeding, ensure you have the correct VPC name that is being used for this project:

Navigate to the <a href="https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#LoadBalancers:sort=loadBalancerName">Load Balancer section of the EC2 Console</a>
- Select the checkbox next to the project name you are working on, select the **Description** tab, and locate the **VPC** attribute (in this format: vpc-xxxxxxxxxxxxxxxxx). **Note:** You will need the VPC attribute when you configure the target groups.

**Configure the Target Groups**

In the terminal, enter the following command to create a target group for each service (posts, threads, and users). In addition, you will create a target group (drop-traffic) to keep traffic from reaching your monolith after your microservices are fully running. Remember to replace the following placeholders: [region], [service-name], and [vpc-attribute].
Service names: **posts**, **threads**, **users**, and **drop-traffic**

$ aws elbv2 create--group --region us-east-1 --name drop-traffic --protocol HTTP --port 80 --vpc-id vpc-0d17419a2e8809480 --healthy-threshold-count 2 --unhealthy-threshold-count 2 --health-check-timeout-seconds 5 --health-check-interval-seconds 6

Mine is 
![](east.png)
![](drop.png)

## Access the listener rules



The <p><a href="(http://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-listeners.html)">listener</a></p>
checks for incoming connection requests to your ALB in order to route traffic appropriately.Right now, the four services (monolith and your three microservices) are running behind the same load balancer. To make the transition from monolith to microservices, we will start routing traffic to your microservices and stop routing traffic to your monolith.
To do that we access the listener rules by 
1. Navigate to the [Load Balancer section of the EC2 Console](https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:).
- Locate the Load Balancer named **demo** and select the checkbox next to it to see the Load Balancer details.
- Select the **Listeners** tab.
**Update Listener Rules**
There should only be one listener listed in this tab. Take the following steps to edit the listener rules:

- Under the **Rules** column, select **View/edit rules**.
- On the **Rules** page, select the plus (**+**) button.The option to **Insert Rule** appears on the page.
- Use the following rule template to insert the necessary rules which include one to maintain traffic to the monolith and one for each microservice:
    - IF Path = /api/[service-name]* THEN Forward to [service-name]For example: IF Path = /api/posts* THEN Forward to posts
    - Insert the rules in the following order:
        - api: */api** forwards to *api*
        - users: */api/users** forwards to *users*
        - threads: */api/threads** forwards to *threads*
        - posts: */api/posts** forwards to *posts*
- Select **Save**.
- Select the back arrow at the top left corner of the page to return to the load balancer console.
![](/list.png)


## Deploy the Microservices

To deploy the three microservices (posts, threads, and users) to the cluster, we will repeat the steps below for each of the three microservice. We begin by 
- Navigating to the [Amazon ECS console](https://console.aws.amazon.com/ecs/home). Select **Clusters** from the left menu bar.
- Select the cluster **BreakTheMonolith-Demo**, select the **Services** tab then select **Create**.
- On the **Configure service** page, edit the following parameters (and keep the default values for parameters not listed below):
    - For the **Launch type**, select **EC2**.
    - For the **Task Definition**, select the **Enter a value** button to automatically select the highest revision value.For example: api:1
    - For the **Service name**, enter a service name (*posts, threads, or users*).
    - For the **Number of tasks**, enter *1*
- Select **Next step**.
![](deploy1.png)


- On the **Configure network** page, **Load balancing** section, do the following:
    - For the **Load balancer type**, select **Application Load Balancer**.
    - For the **Service IAM role**, select **BreakTheMonolith-Demo-ECSServiceRole**.
    - For the **Load balancer name**, verify that **demo** is selected.
    - In the **Container to load balance** section, select the **Add to load balancer** button and make the following edits:
        - For the **Production listener port**, set to **80:HTTP**.
        - For the **Target group name**, select the appropriate group: *(***posts**, **threads**, or **users**)
- Select **Next step**.

!(deploy2.png)

- On the **Set Auto Scaling** page, select **Next step**.
- On the **Review** page, select **Create Service**.
- Select **View Service**.
It should only take a few seconds for all the services to start. Double check that all services and tasks are running and active before you proceed.

![](deploy3.png)

Now the microservices are now running, but all traffic is still flowing to your monolith service. To reroute traffic to the microservices, we will now update the listener rules by carrying out the steps below:

- Navigate to the [Load Balancers section of the EC2 Console](https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:).
- Select the checkbox next to **demo** to see the Load Balancer details.
- Select the **Listeners** tab.There should only be one listener listed.
- Under the **Rules** column, select **View/edit rules**.
- On the **Rules** page, select the minus (****) button from the top menu.
- Delete the first rule (*/api* forwards to api*) by selecting the checkbox next to the rule.
- Select **Delete**.
- Update the default rule to forward to drop-traffic:
    - Select the edit (pencil) button from the top menu.
    - Select the edit (pencil) icon next to the default rule (**HTTP 80: default action**).
    - Selec the edit (pencil) icon in the **THEN** column to edit the **Forward to**.
    - In the **Target group** field, select **drop-traffic**.
    - Select the **Update** button.
    ![](/rules1.png)

    **Disable the monolith:** With traffic now flowing to your microservices, you can disable the monolith service.

- Navigate back to the Amazon ECS cluster **BreakTheMonolith-Demo-ECSCluster**.
- In the **Services** tab, select the checkbox next to **api** and select **Update**.
- On the **Configure service** page, locate **Number of tasks** and enter *0*.
- Select **Skip to review**.
- Select **Update Service**.

Amazon ECS will now empty connections from containers the service has deployed on the cluster then stop the containers. If you refresh the Deployments or Tasks lists after about 30 seconds, you will see that the number of tasks will drop to 0. The service is still active, so if you needed to roll back for any reason, you could simply update it to deploy more tasks.

Optionally, you can delete the api service. In the **Services** tab, select the checkbox next to **api**, select **Delete**, and confirm the deletion.

**You have now fully transitioned your node.js from the monolith to microservices, without any downtime!**

**Find your service URL**: This is the same URL that you used in Module 2 of this tutorial.

- Navigate to the [Load Balancers section of the EC2 console](https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:).
- Select the checkbox next to **demo** to see the Load Balancer details.
- In the **Description** tab, locate the **DNS name** and select the copy icon at the end of the URL.
- Paste the DNS name into a new browser tab or window.

You should see a message 'Ready to receive requests'.

**See the values for each microservice:** Your ALB routes traffic based on the request URL. To see each service, simply add the service name to the end of your DNS name:

- http://[DNS name]/api/users
- http://[DNS name]/api/threads
- http://[DNS name]/api/posts
![](/disable.png)

## Module Five - Clean Up

In this module, you will terminate the resources you created during this tutorial. You will stop the services running on Amazon ECS, delete the ALB, and delete the AWS CloudFormation stack to terminate the ECS cluster, including all underlying EC2 instances.

Cleaning up is not required, but will help you avoid ongoing charges for keeping these services running.

**Services Used:**

- [Amazon Elastic Container Service](https://aws.amazon.com/ecs/)
- [Amazon Elastic Container Registry](https://aws.amazon.com/ecr/)
- [Amazon EC2](https://aws.amazon.com/ec2/)
- [Amazon VPC](https://aws.amazon.com/vpc/)
- [Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing/applicationloadbalancer/)

---

## Clean Up Instructions

Follow the instructions below to delete the AWS resources you created in each module.

Start clean up by deleting each of the services (posts, threads, abd users) that are running in your cluster:


- Navigate to the [Amazon ECS console](https://console.aws.amazon.com/ecs/home?) and select **Clusters**.
- Select the **BreakTheMonolith-Demo** cluster.
- In the **Services** tab, select a service and then select **Delete**.
- Confirm the deletion.
- Repeat the steps until all the services are deleted.
![](delete.png)
Before proceeding to the next step, you need to either wait for all running tasks to terminate or select the **Tasks** tab and select **Stop All**.

Repeat these steps for each of your services on the cluster.

Navigate to the [Load Balancer section of the EC2 Console.](https://console.aws.amazon.com/ec2/v2/home?#LoadBalancers:)

- Select the checkbox next to **demo** and select the **Listeners** tab.
- Select the listener, then select **Delete**.

![[](/delete2.png)
- Confirm the deletion.Navigate to [Target Groups](https://console.aws.amazon.com/ec2/v2/home?#TargetGroups:) in the EC2 console.Check the checkbox at the top of the list (next to **Name**) to select all target groups.Select **Actions** then select **Delete**.Confirm the deletion.
![[](/delete3.png)
Navigate to the [AWS CloudFormation console](https://console.aws.amazon.com/cloudformation/home?).

- Check the box next to the Cloudformation stack **BreakTheMonolith-Demo**.
- Select **Actions** then select **Delete Stack**.
- Confirm the deletion.
- The stack status should change to DELETE_IN_PROGRESS*.*

**⚠** **WARNING!** Leaving a stack running will result in charges on your AWS account.

![[](/delete4.png)
Navigate to [Task Definitions](https://console.aws.amazon.com/ecs/home?#/taskDefinitions) in the Amazon ECR console.

- Select a task definition (api, posts, threads, or users).
- On the **Task Definition Name** page, select the checkbox next to the task name.
- Select **Actions** then from the drop-down list select **Deregister**.
- Confirm your action.

Repeat these steps for all four task definitions.

Navigate to [Repositories](https://console.aws.amazon.com/ecs/home?#/repositories) in the Amazon ECR console.

- Select the checkbox next to a repository and then select **Delete**.
- Confirm the deletion.
- Repeat the steps until all the repositories are deleted.

![](/apid.png)

****Congratulations:****

# We Just Broke the Monolith

**Nice Work! We have completed the project and split a monolithic app into containerized microservices using Amazon Web Services (AWS).**

