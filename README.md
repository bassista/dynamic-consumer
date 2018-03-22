# Dynamics Camel Consumers Example

#### A simple example to demonstrate how to use a list of endpoints defined in a configuration to create consumer routes for each of them at runtime.

Given this configuration:

    application.properties
    folderNames: test1, test2, test3

And this Camel route builder:

        for (String folderName : folderNames) {
            from("file://" + folderName)
                    .to("direct:processFiles");
        }

        from("direct:processFiles")
                .log("found file >>> ${headers.CamelFileName}");    
    
During startup, Camel will create 3 consumer routes to consume from test1, test2, test3 folders. Any file found in these folders, will be send to a common processFiles route.


#### Here are the runtime routes generate from the above code (notice there are 4 routes in total):

![runtime routes](https://raw.githubusercontent.com/bibryam/dynamic-consumer/master/runtime-route.png)


#### And here are the routes visualizes in Hawtio webconsole deployed to OpenShift

![runtime routes visualized](https://raw.githubusercontent.com/bibryam/dynamic-consumer/master/runtime-routes-visual.png)


#### Run:
    mvn spring-boot:run -s configuration/settings.xml 
 