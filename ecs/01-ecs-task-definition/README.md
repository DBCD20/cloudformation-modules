# ECS Task Definition

A task definition is a blueprint for your application. It is a text file in JSON format that describes the parameters and one or more containers that form your application.

## Pre Requisite:
* Fargate ECS Cluster
* VPC

This template provisions the following resources:
* ECS Task Definition

## Running the template
### * Validating the template
Always run validate template each time you make changes with the code.
```
aws cloudformation validate-template --template-body file://template.yaml
```

### * How to provision

* Create a file that contains your parameter e.g `params.json` the following are the valid parameters to consider:

    * `ApplicationName` Your application name, this will appear on your task definition
    * `Port` Port to open to receieve and send traffic to.
    * `ImageName` The image used to start a container. This string is passed directly to the Docker daemon. By default, images in the Docker Hub registry are available. 
    * `Cpu` The number of cpu units used by the task. If you use the EC2 launch type, this field is optional. The CPU units cannot be less than 1 vCPU when you use Windows containers on Fargate.
    * `Memory` The amount (in MiB) of memory used by the task.
    * `TaskDefinitionFamily` The name of a family that this task definition is registered to. Up to 255 letters (uppercase and lowercase), numbers, hyphens, and underscores are allowed.
    

Using the terminal type the following commands:
```
aws cloudformation deploy \
--template-file template.yaml \
 --stack-name  test-ecs-svc-template \
--parameter-overrides file://<Your file name>.json
```

### * How to delete stack

Using the terminal type the following commands:
```
 aws cloudformation delete-stack --stack-name <Your-stack-name>
```

### * Troubleshooting Guide

If ever during your deployment, you encounter the following error below, check the events to see the root cause

```
Failed to create/update the stack. Run the following command
to fetch the list of events leading up to the failure
```

Then run the command below to see events or using using the browser.
```
aws cloudformation describe-stack-events --stack-name <Your Stack>
```