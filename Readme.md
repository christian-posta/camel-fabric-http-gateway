# Fabric8 Gateway

The [Fabric8](http://fabric8.io) project -- pronounced __fabricate__ --  is a practical DevOps framework for services running on the JVM. Things like automated deployment and centralized configuration management come out of the box and are consistent regardless of JVM container (or no container -- microservices) you use. 
  
One of the other cool features that [Fabric8](http://fabric8.io) gives you out of the box is the ability to dynamically lookup, load balance, and version your services (MQ, REST/http SOAP/http, etc). Clients that live within a "fabric" created by "fabric8" can automatically take advantage of this. Your external clients can too with the [Fabric8 Gateway](http://fabric8.io/gitbook/gateway.html) feature. When combined with [Apache Camel](http://camel.apache.org) routes that expose [CXF](http://cxf.apache.org) you can get very powerful discovery using Fabric8.

This project comes with some dummy deployments that you can use to exercise and test out the gateway for yourself.

## How To

First, start by [grabbing Fabric8](http://fabric8.io/getstarted/index.html) or its downstream, supported by Red Hat, cousin: [JBoss Fuse](http://www.jboss.org/products/fuse/overview/). 

### Start it up:
    
    fabric8-home$  ./bin/fabric8
    
### Or on JBoss Fuse:

    fuse-home$  ./bin/fuse
    
### Next, you'll need to build this project:

    project-home$  mvn clean install
    
And navigate to one of the subprojects (example: beer-service)

Now you'll have to invoke the fabric8-maven-plugin to install the profile into Fabric8/JBoss Fuse. See [the fabric8-maven-plugin](http://fabric8.io/gitbook/mavenPlugin.html) for more details on what it does and how to set it up:

    beer-service$  mvn fabric8:deploy
    
Now navigate to the web console (http://localhost:8181) and go to the _Wiki_ tab. 
You should see your profile there under the _loadbalancer_ group:
 
 ![picture of profiles](http://christian-posta.github.io/images/beer-service-wiki.png)
 
### Now create a new container with that profile.

![picture of profiles](http://christian-posta.github.io/images/create-new-beer.png)

### You should have a new beer container:

![picture of profiles](http://christian-posta.github.io/images/container-list-beer.png)

### Now add a new container and give it the _http gateway_ profile:

![picture of profiles](http://christian-posta.github.io/images/create-new-gateway.png)

### Now you have your beercontainer and your http gateway container:

![picture of profiles](http://christian-posta.github.io/images/list-gateway-beer.png)

### Now you can ping the beer service through the gateway at: http://localhost:9000/cxf/beer:

![picture of profiles](http://christian-posta.github.io/images/final-output-beer.png)

