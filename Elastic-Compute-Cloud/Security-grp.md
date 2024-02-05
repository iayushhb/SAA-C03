# Security Groups and Bootstrap Scripts

>Note -
> - Linux : SSH - PORT 22
> - Windows : RDP - PORT 3389
> - HTTP : WEB BROWSING - PORT 80
> - HTTPS : ENCRYPTED WEB BROWSING (SSL) - 443

## Security Groups : 
Security groups are virtual firewalls for your ec2 isntances . By default , everything is blocked.

**To let everything in : 0.0.0.0/0**

*In order to communicate with your ec2 instances via SSH/RDP/HTTP, you will need to open up the correct ports.*

## Bootstrap scripts : 
A script that runs when an instance first runs.

Ex : 
```
#!/bin/bash
yum install httpd -y 
#installs apache
yum service httpd start 
#starts apache
```
*Adding these tasks at boot time adds to the amount of time it takes to boot the instance.
However, it allows you to automate the installation of applications.*

### Now let's use scripting
1. Head over to ec2 and hit launch instance 
2. Create security grp rules 
![Alt text](/Photos/ec2-security-grp.png)
3. Then go to the advanced details and scroll to the bottom and paste this script : 
```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
cd /var/www/html
echo "<html><body><h1>Hello Cloud Gurus</h1></body></html>" > index.html
```
Now hit create.

![Alt text](/Photos/sec-grp-details.png)
When your ec2 instance starts running then select the instance and and copy the `Public IPv4 address` and paste it into your browser and done.
