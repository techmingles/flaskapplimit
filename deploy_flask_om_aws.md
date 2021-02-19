## Deploying a flask application to Elastic Beanstalk

Initialize your EB CLI repository with the eb init command:
```
~/eb-flask$ eb init -p python-3.6 flaskapplimit --region us-east-2
```
Application flaskapplimit has been created.
This command creates a new application named flaskapplimit and configures your local repository to create environments with the latest Python 3.6 platform version.


(optional) Run eb init again to configure a default keypair so that you can connect to the EC2 instance running your application with SSH:
```
~/eb-flask$ eb init
Do you want to set up SSH for your instances?
(y/n): y
Select a keypair.
1) my-keypair
2) [ Create new KeyPair ]
```

Select a key pair if you have one already, or follow the prompts to create a new one. If you don't see the prompt or need to change your settings later, run eb init -i.

Create an environment and deploy your application to it with eb create:
```
~/eb-flask$ eb create flask-env
```
Environment creation takes about 5 minutes and creates the following resources:

EC2 instance – An Amazon Elastic Compute Cloud (Amazon EC2) virtual machine configured to run web apps on the platform that you choose.

Each platform runs a specific set of software, configuration files, and scripts to support a specific language version, framework, web container, or combination of these. Most platforms use either Apache or NGINX as a reverse proxy that sits in front of your web app, forwards requests to it, serves static assets, and generates access and error logs.

Instance security group – An Amazon EC2 security group configured to allow inbound traffic on port 80. This resource lets HTTP traffic from the load balancer reach the EC2 instance running your web app. By default, traffic isn't allowed on other ports.

Load balancer – An Elastic Load Balancing load balancer configured to distribute requests to the instances running your application. A load balancer also eliminates the need to expose your instances directly to the internet.

Load balancer security group – An Amazon EC2 security group configured to allow inbound traffic on port 80. This resource lets HTTP traffic from the internet reach the load balancer. By default, traffic isn't allowed on other ports.

Auto Scaling group – An Auto Scaling group configured to replace an instance if it is terminated or becomes unavailable.

Amazon S3 bucket – A storage location for your source code, logs, and other artifacts that are created when you use Elastic Beanstalk.

Amazon CloudWatch alarms – Two CloudWatch alarms that monitor the load on the instances in your environment and that are triggered if the load is too high or too low. When an alarm is triggered, your Auto Scaling group scales up or down in response.

AWS CloudFormation stack – Elastic Beanstalk uses AWS CloudFormation to launch the resources in your environment and propagate configuration changes. The resources are defined in a template that you can view in the AWS CloudFormation console.

Domain name – A domain name that routes to your web app in the form subdomain.region.elasticbeanstalk.com.

All of these resources are managed by Elastic Beanstalk. When you terminate your environment, Elastic Beanstalk terminates all the resources that it contains.

Note
The Amazon S3 bucket that Elastic Beanstalk creates is shared between environments and is not deleted during environment termination. For more information, see Using Elastic Beanstalk with Amazon S3.

When the environment creation process completes, open your web site with eb open:

```
~/eb-flask$ eb open
```

This will open a browser window using the domain name created for your application. You should see the same Flask website that you created and tested locally.


If you don't see your application running, or get an error message, see Troubleshooting Deployments for help with how to determine the cause of the error.

If you do see your application running, then congratulations, you've deployed your first Flask application with Elastic Beanstalk!

Cleanup
When you finish working with Elastic Beanstalk, you can terminate your environment. Elastic Beanstalk terminates all AWS resources associated with your environment, such as Amazon EC2 instances, database instances, load balancers, security groups, and alarms.

To terminate your Elastic Beanstalk environment

Open the Elastic Beanstalk console, and in the Regions list, select your AWS Region.

In the navigation pane, choose Environments, and then choose the name of your environment from the list.

Note
If you have many environments, use the search bar to filter the environment list.

Choose Environment actions, and then choose Terminate environment.

Use the on-screen dialog box to confirm environment termination.

With Elastic Beanstalk, you can easily create a new environment for your application at any time.

Or, with the EB CLI:

```
~/eb-flask$ eb terminate flask-env
```
