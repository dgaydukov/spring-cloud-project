# Spring Cloud projects docs

### Content
* [Project Description](#project-description)
* [Available Repositories](#available-repositories)
* [Service Discovery](#service-discovery)
* [Open Telemetry](#open-telemetry)

### Project Description
This project is like an umbrella for all spring-cloud related projects where all docs would be collected, about how they work with each other. Why do we need separate docs project for this. Spring cloud helps us to connect multiple services into single entity, yet there are some rules for connecting them. And the problems where do you add details how to connect multiple services together. If you add it into one project it may be confusing, but if you duplicate it inside multiple services it's redundant. For this reason I've created a separate projects with docs-only details. This project would include:
* detailed docs on each ms that participate in cloud connection
* docker-compose files, if additional dependencies are required
* tech stack description - why did we choose one technology over another

### Available Repositories
There are 3 repo under spring-cloud umbrella:
* [spring-cloud-external-gateway](https://github.com/dgaydukov/spring-cloud-external-gateway) - as name suggests this is the gateway project which is serving requests from outside the cloud. All your projects can talk inside VPC (virtual private network in AWS) directly to each other, no additional auth layer is required, but if you want to access any service from outside, you need gateway which provides: auth layer + data aggregation layer. 
* [spring-cloud-asset-service](https://github.com/dgaydukov/spring-cloud-asset-service) - simple spring-boot service with several API endpoints to get assets & prices
* [spring-cloud-order-service](https://github.com/dgaydukov/spring-cloud-order-service) - simple spring-boot service with several API endpoints to created & fetch orders

### Service Discovery
One of the most important feature of any MS architecture is service discovery. Services inside MS architecture need to communicate with one another, and they call each other by either DNS name or IP+port. So they need to know addresses of each other. You can manually assign address to each MS and then pass it as env vars to all MS, but it's not a good idea. Ideally if services can just call each other by the name, and under-the-hood they can find each other IP & port. This is exactly what is service discovery for. You just add it, and inside your code you can call each other just by name.

### Open Telemetry