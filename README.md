# Spring Cloud projects docs

### Content
* [Project Description](#project-description)
* [Available Repositories](#available-repositories)
* [Microservice architecture](#microservice-architecture)
* [Best practices](#best-practices)
* [Service Discovery](#service-discovery)
* [Open Telemetry](#open-telemetry)

### Project Description
This project is like an umbrella for all spring-cloud related projects where all docs would be collected, about how they work with each other. Why do we need separate docs project for this. Spring cloud helps us to connect multiple services into single entity, yet there are some rules for connecting them. And the problems where do you add details how to connect multiple services together. If you add it into one project it may be confusing, but if you duplicate it inside multiple services it's redundant. For this reason I've created a separate projects with docs-only details. This project would include:
* detailed docs on each ms that participate in cloud connection
* docker-compose files, if additional dependencies are required
* tech stack description - why did we choose one technology over another

### Available Repositories
>Important: all 3 services requiring the nacos to be running first, otherwise they won't be able to start. Plz make sure you successfully run nacos locally through the docker, then you can run any of these 3 apps.

There are 3 repo under spring-cloud umbrella:
* [spring-cloud-external-gateway](https://github.com/dgaydukov/spring-cloud-external-gateway) - as name suggests this is the gateway project which is serving requests from outside the cloud. All your projects can talk inside VPC (virtual private network in AWS) directly to each other, no additional auth layer is required, but if you want to access any service from outside, you need gateway which provides: auth layer + data aggregation layer. 
* [spring-cloud-asset-service](https://github.com/dgaydukov/spring-cloud-asset-service) - simple spring-boot service with several API endpoints to get assets & prices
* [spring-cloud-order-service](https://github.com/dgaydukov/spring-cloud-order-service) - simple spring-boot service with several API endpoints to created & fetch orders

### Microservice architecture
Currently inside 3 available repos we have:
* service discovery - we use [nacos](Nacos.md) so services can register itself on start-up and talk to each other by name (no need to hardcode IP addresses of each service)
* global config management - we use [nacos](Nacos.md) to store global config for all micro-services, which simplify it management, and also allows hot reload 
* i18n - we have added support for multiple languages, and header propagation. If you want to get response in specific language, just pass header in your request `Accept-Language: es`. Because we use header propagation, if A->B->C, and you call service A with this header, your header would be propagated all the way to C, and you get response form C in your selected language
* OpenTelemetry and tracing - we are using [mictometer tracing](https://spring.io/blog/2022/10/12/observability-with-spring-boot-3) to add support for tracing. Now traceId is inserted into all logs, and also propagated through service chain call. Now you can use single traceId to fetch all logs from all services which were part of this request execution.

### Best practices
In this example, in all 3 services we are using best practice approach which include:
* code validation with check-style plugin - you can read [docs](https://checkstyle.org/checks/sizes/linelength.html#LineLength) about existing checks that are possible to add into checkstyle.xml file. Then these checks are validated on `mvn clean install` goal to make sure that if checks are violated, the code won't compile
* use of `gRPC` protocol of internal communication between services. For client-facing endpoints `REST API` is preferable, cause clients get used to use REST json communication. But services when communicating with each other should use `gRPC` cause it faster and better for intra-service communication.

### Service Discovery
One of the most important feature of any MS architecture is service discovery. Services inside MS architecture need to communicate with one another, and they call each other by either DNS name or IP+port. So they need to know addresses of each other. You can manually assign address to each MS and then pass it as env vars to all MS, but it's not a good idea. Ideally if services can just call each other by the name, and under-the-hood they can find each other IP & port. This is exactly what is service discovery for. You just add it, and inside your code you can call each other just by name.
There are several tools to enable service-discovery including: `nacos`, `eureka` and others. For this project demo I've chosen `nacos` as an example. And although configuration is different for each project, but once you configure it, the logic is always the same, you just add service-name to the Feign config, and it works out-of-the-box.
You can find more details in [nacos page](Nacos.md).

### Open Telemetry
This one is the most important part in the system, cause not only it helps a lot to devs, but it also add customer's value by helping to monitor the app, track any problems, and trace any user journey.
You can find more info on [OpenTelemetry website](https://opentelemetry.io/docs/what-is-opentelemetry), this is official web-page with detailed explanation what is OpenTelemetry is about. Here I just say that open telemetry include 3 things:
* logs
* metrics
* traces
You can find more details in [tracing page](otel/Tracing.md).