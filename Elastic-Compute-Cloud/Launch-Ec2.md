# Launching an EC2 Instance (Demo)

1. Head over to compute > ec2.
![Alt text](/Photos/ec2-dashboard.png)
2. Now hit launch instance.
3. Fill name of the instance and select `Amazon Linux` for AMI.
4. Select ec2-micro for instance type.
5. Then hit Create new key pair and it will download a file onto your system.
![Alt text](/Photos/ec2-key-pair.png)
6. Every ec2 instance is provisioned behind the security group, security group is nothing but a virtual firewall.
Now check `Allow HTTPS traffic from the internet` and `Allow HTTP traffic from the internet`.
7. Now hit launch instance.

## Connecting to EC2 instance 
![Alt text](/Photos/ec2-connection.png)
To connect to the ec2 instance select the instance and hit connect and use ec2 instance connect and hit connect.
![Alt text](/Photos/amazon-linux.png)

## Termination
To terminate your instance you simply have to select the instance hit instance state and click terminate instance.