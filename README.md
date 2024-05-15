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
* [spring-cloud-external-gateway](https://github.com/dgaydukov/spring-cloud-external-gateway)
* [spring-cloud-asset-service](https://github.com/dgaydukov/spring-cloud-asset-service)
* [spring-cloud-order-service](https://github.com/dgaydukov/spring-cloud-order-service)

### Service Discovery

### Open Telemetry