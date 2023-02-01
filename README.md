# AWS CLI Cheatsheet

This repo is a collection of AWS CLI queries, organized by service. 

## VPC

**Returns the vpc-id for the default VPC**

`aws ec2 describe-vpcs --filter Name=is-default,Values=true --query Vpcs[].VpcId --output text`

**Returns the subnet-id for a subnet with the following tag: Type,Values=Private**

`aws ec2 describe-subnets --filters Name=tag:Type,Values=Private --query "Subnets[*].SubnetId" | jq -r '.[0]'`

**Returns the group-id for a security group with the following tag: Type,Values=WebServerSG**

`aws ec2 describe-security-groups --filters "Name=tag:Name,Values=WebServerSG" --query "SecurityGroups[*].GroupId" | jq -r '.[0]'`


## EC2

**Returns the ARN for a load balancer named FargateALB**

`aws elbv2 describe-load-balancers --names FargateALB --query "LoadBalancers[*].LoadBalancerArn" | jq -r '.[0]')`

**Returns the ARN for a target group named HTTPTargetGroup**

`aws elbv2 describe-target-groups --name HTTPTargetGroup --query "TargetGroups[*].TargetGroupArn" | jq -r '.[0]')`

**Describe instances concisely**

`aws ec2 describe-instances | jq '[.Reservations | .[] | .Instances | .[] | {InstanceId: .InstanceId, State: .State, SubnetId: .SubnetId, VpcId: .VpcId, Name: (.Tags[]|select(.Key=="Name")|.Value)}]'`

**Returns instance ID**

`wget -q -O - http://169.254.169.254/latest/meta-data/instance-id`



## IAM

**Creates a new Access Key Pair and saves the SecretAccessKey to a variable**
`ECRUSERSECRETACCESSKEY=$(aws iam create-access-key --user-name myUser | jq -r '.[].SecretAccessKey')`


## ELBv2

**Gets the DNS name of an ALB**
aws elbv2 describe-load-balancers | jq -r '.LoadBalancers | .[].DNSName'
