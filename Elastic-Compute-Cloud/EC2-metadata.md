# EC2 Metadata & Userdata
EC2 metadata is simply data about your EC2
instance. 

This can include information such as private IP address, public IP
address, hostname, security groups, etc.

*Using the `curl` command we can query metadata about our ec2 instance.*

And also, with a simple bootstrap(user data) script we can use the curl command to save our ec2 metadata.

## Implementation -
1. Create an ec2 instance and paste this bootstrap script. and add http ,https and ssh as security rules. and enable metadata and select what IDMS(Instance Metadata Service) version you wanna use.

**For IMDSv1**

*Use Amazon Linux 2 instance*
```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
cd /var/www/html
echo "<html><body><h1>My IP is" > index.html 
curl http://169.254.169.254/latest/meta-data/public-ipv4 >> index.html
echo "</h1></body></html>" >> index.html
```

**For IMDSv2**

*Use Amazon Linux 2023 instance*
```
#!/bin/bash
yum update -y
yum install httpd -y
systemctl start httpd
systemctl enable httpd
cd /var/www/html
echo "<html><body><h1>My IP is" > index.html 
TOKEN=$(curl -s -X PUT "http://169.254.169.254/latest/api/token" -H "X-aws-ec2-metadata-token-ttl-seconds: 21600")
PUBLIC_IP=$(curl -s -H "X-aws-ec2-metadata-token: $TOKEN" http://169.254.169.254/latest/meta-data/public-ipv4)
echo "$PUBLIC_IP" >> index.html
echo "</h1></body></html>" >> index.html
```
2. Now copy your public-ip4 ip and paste it in browser. 
![Alt text](/Photos/metadata-page.png)
