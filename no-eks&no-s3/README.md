create stack
```
aws cloudformation create-stack --stack-name vpc-stack --template-body file://3AZ-VPC.yml --capabilities CAPABILITY_IAM
```

etc
```
- 3AZ-VPC.yml
- 3AZ-3Teir-VPC.yml
- 3AZ-VPC-GW.yml
- 3AZ-3Teir-VPC-GW.yml

- 2AZ-VPC.yml
- 2AZ-3Teir-VPC.yml
- 2AZ-VPC-GW.yml
- 2AZ-3Teir-VPC-GW.yml
```

Parameter information
```
fw-LogGroup -> cloudwatch-logs
```

bastion
```
#!/bin/bash
sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
sed -i 's/#Port 22/Port 2024/g' /etc/ssh/sshd_config
echo 'password' | passwd --stdin ec2-user
systemctl restart sshd
```

install package
```
#docker install
yum install docker -y
sudo systemctl restart docker
usermod -aG docker ec2-user
systemctl restart docker

# jq install
yum install jq -y

# git install
yum install git -y

#awscli install
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
mv /usr/local/bin/aws /bin/
```