# ECS

ECS allows us to run containerized application without worrying of infrastructure (Fargate) or with minimal overhead (EC2 Instance). It is a container orchestrating tool that works in a declarative manner. It manages your container by maintaining the desired state that you declare on your task definition.

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

### Definition of terms:

* `ECS` Amazon Elastic Container Service (Amazon ECS) is a fully managed container orchestration service that helps you easily deploy, manage, and scale containerized applications.
* `Task Definition` A task definition is a blueprint for your application. It is a text file in JSON format that describes the parameters and one or more containers that form your application.
* `ECS Service` Runs and maintains the requested number of tasks and associated load balancers.

## ECS in cloudformation

The way we provision infrastructure in AWS is thru cloudformation, We practice infrastructure as code to maintain and update our infrastructure in a reusable and repeatable manner.

    How to provision:

    To provision cluster, you must choose on whether you want or you have the capacity to manage infrastructure.

#### Difference between ec2 and fargate (serverless) cluster

* `ec2 instance`creating cluster using ec2 instance allows you to have cost savings but with some management on your side
* `fargate` No manage servers but comes with a price


### Before you Provision

Make sure to have a vpc created with dedicated subnets (specially private subnets). Route table should be registered diligently specially routes where image will be pulled.

Once you're decided, go to the folder with `00-` and follow the instructions inside it. the flow of provisioning ecs resouce is by:

1. ECS Cluster
2. ECS Task Definition
3. ECS Service

