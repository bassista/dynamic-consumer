# Dynamics Camel Consumers Example

#### Demonstrate how to use a list of endpoints coming from a configuration to create consumer routes for them.

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

#### Run:
    mvn spring-boot:run -s configuration/settings.xml 
 