# Virtual Private Network

## Gateways

1. __NAT gateway__ enables outbound-only Internet communication over IPv4.
2. __Egress-Only Internet Gateway__ enables outbound-only Internet communication over IPv6.
3. __Internet Gateway__ enalbes two-way Internet communication. It supports both IPv4 and IPv6.

VPC and subnets don't have the ability to communicate with the public Internet by default. Some type of gateway needs to be configured. And route table and routes need to be created as well. Steps:

1. Create a gatway(NAT, egress-only IG or regular IG).
2. Create a routable in VPC.
3. Create a route that points to the gateway.

Then traffic from inside the VPC can find its way out to the world.
