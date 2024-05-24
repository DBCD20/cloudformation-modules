# ECS Service

This template resource creates an Amazon Elastic Container Service (Amazon ECS) service that runs and maintains the requested number of tasks and associated load balancers.

## Pre Requisite:
* Fargate ECS Cluster
* Task Definition

## Resources provisioned:
* ECS Service
* Application Load Balancer
* Security group for load balancer
* Load balancer target group
* Load balancer listener
* Load balancer listener rule

## Parameters

|ParameterKey  | Value Type | Allowed Values  | 
|---|---|---|
| ApplicationName               |   <i>String</i>               |   e.g my-application              |
| ContainerName                 |   <i>String</i>               |   ap-southeast-1                  | 
| ContainerPort                 |   <i>Number</i>               |   e.g 80                          |
| DesiredCount                  |   <i>Number</i>               |   e.g 1                           |
| HealthCheckGracePeriodSeconds |   <i>Number</i>               |   e.g 60                          |
| DeploymentController          |   <i>String</i>               |   "CODE_DEPLOY", "ECS", "EXTERNAL"| 
| EnableExecuteCommand          |   <i>String</i>               |  "Yes", "No"                      | 
| PrivateSubnetIds              | List<AWS::EC2::Subnet::Id>    |  subnet-123, subnet-456           | 
| PublicSubnetIds               | List<AWS::EC2::Subnet::Id>    |  subnet-123, subnet-456           | 
| ExistingListener              |   <i>String</i>               |   e.g existing-alb-listener       | 
| ALBListenerProtocol           |   <i>String</i>               |   ["HTTP", "HTTPS"]               | 
| ALBListenerPort               |   <i>Number</i>               |   e.g 80                          | 
| ExistingTargetGroup           |   <i>String</i>               |   e.g existing-tg                 | 
| TGName                        |   <i>String</i>               |   e.g my-target-group             | 
| TGHealthCheckProtocol         |   <i>String</i>               |   e.g HTTP                        | 
| TaskDefinition                |   <i>String</i>               |   e.g my-httpd:2                  | 
| ServiceName                   |   <i>String</i>               |   e.g my-ecs-name                 | 
| ClusterName                   |   <i>String</i>               |   e.g ecs-develop-cluster         | 
| EnableExecuteCommand          |   <i>String</i>               |   [Yes, No]                       | 
| LoadBalancer                  |   <i>String</i>               |   my-existing-load-balancer       | 
| VPCId                         |   <i>String</i>               |   vpc-123456                      | 
| VpcCidrBlock                  |   <i>String</i>               |   e.g 10.0.0.0/16                 | 
| LoadBalancerScheme            |   <i>String</i>               |   [nternet-facing, internal ]     | 

## How to provision template

HIP Team will copy the parameters.json to the project's IAC Repository. Project team will update the parameters json base on the available [parameters](#parameters-and-its-valid-values) in their own project repository.