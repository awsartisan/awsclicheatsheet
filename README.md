# AWS CLI Cheatsheet

This repo is a collection of AWS CLI queries, organized by service. 

## VPC

**Returns the vpc-id for a VPC with the following tag: Name,Values=Lab-VPC**

`aws ec2 describe-vpcs --filter Name=tag:Name,Values=Lab-VPC --query Vpcs[].VpcId --output text`

**Returns the subnet-id for a subnet with the following tag: Type,Values=Private**

`aws ec2 describe-subnets --filters Name=tag:Type,Values=Private --query "Subnets[*].SubnetId" | jq -r '.[0]'`

**Returns the group-id for a security group with the following tag: Type,Values=WebServerSG**

`aws ec2 describe-security-groups --filters "Name=tag:Name,Values=WebServerSG" --query "SecurityGroups[*].GroupId" | jq -r '.[0]'`


## EC2

**Returns the ARN for a load balancer named FargateALB**

`aws elbv2 describe-load-balancers --names FargateALB --query "LoadBalancers[*].LoadBalancerArn" | jq -r '.[0]')`

**Returns the ARN for a target group named HTTPTargetGroup**

`aws elbv2 describe-target-groups --name HTTPTargetGroup --query "TargetGroups[*].TargetGroupArn" | jq -r '.[0]')`
