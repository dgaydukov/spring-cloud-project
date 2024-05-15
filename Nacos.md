# Nacos

### Description
This is a service discovery solution that helps:
* service discovery - you can connect your services to each other using this solution, once your service is started it can register itself within this service discovery solution by it's name, and if any other service wants to call it, you just pass it's name. Pay attention that here when we define annotation we don't pass url, we just pass service name, and the URL would be fetched from Nacos
```java
@FeignClient(name = "product-service")
```
* config management - this can be helpful if we want to introduce global config management for all of our apps

### Installation
Nacos is a server that running with specific port, so if you want to use it, you need to first install it. Here is a good [docs](https://nacos.io/en-us/docs/quick-start-docker.html) how to set-up nacos locally from the docker