# Fargate

## Types of fargate

1. Deploy as a service
2. Deploy as a task

## Requirement

- VPC and subnets:
    VPC and subnets need to be created for either service or task, so that resource can be allocated for fargate.
- VPC needs a route in route table to an Internet Gateway so that it can pull the docker image from ECR or external registry.
- A service requires a load balancer. So a load balancer needs to be created in EC2 console and associated with the VPC. This needs to be done in advance of running a service. __NOTE__: A load balancer by default has a closed security group. So it doesn't accept public traffic by default.
- Make sure the service has a health check endpoint.
- When one is creating the fargate service, a target group will be newly configured and generated under the previous created load balancer.

## __NOTE__: Common errors

1. Docker image can't be pulled and contain failed at start-up: VPC doesn't have a route to the public Internet. Add a route to igw in VPC route table.
2. Docker image constantly restarts: Health check failed.
3. Service can't be accessed with ELB address but individual instances are accessible: ELB security group setting.
