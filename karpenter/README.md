References
- elb region code: https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/enable-access-logs.html

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
ClusterName -> skills-cluster
BucketStorage -> bucket-aaaa213123
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

#kubernetes install version 1.27
curl -LO https://dl.k8s.io/release/v1.27.4/bin/linux/amd64/kubectl
chmod +x ./kubectl
sudo mv ./kubectl /bin/kubectl


#kubernetes bash-completion
source /usr/share/bash-completion/bash_completion
echo 'source <(kubectl completion bash)' >>~/.bashrc
echo 'alias k=kubectl' >>~/.bashrc
echo 'complete -o default -F __start_kubectl k' >>~/.bashrc
exec bash

#eksctl install(latest)
ARCH=amd64
PLATFORM=$(uname -s)_$ARCH
curl -sLO "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"
curl -sL "https://github.com/eksctl-io/eksctl/releases/latest/download/eksctl_checksums.txt" | grep $PLATFORM | sha256sum --check
tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz
sudo mv /tmp/eksctl /usr/local/bin

#helm install version v3.12.0 ( k8s 1.26 ~ 1.27 )
wget https://get.helm.sh/helm-v3.12.0-linux-amd64.tar.gz
tar zxvf helm-v3.12.0-linux-amd64.tar.gz
mv linux-amd64/helm /bin/

#awscli install
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
mv /usr/local/bin/aws /bin/

# jq install
yum install jq -y

# git install
yum install git -y
```