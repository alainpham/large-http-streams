large-http-streams
=========================================

This projects shows how you can setup http services with minimal configuration that are able to handle 
large streams of data without encountering memory issues.
It uses the camel-http4 component for sending data and the camel-jetty component to receive.


Blog article for more details about handling large stream will come soon on :
https://alainpham.github.io


To build this project use

    mvn install

To make sure that it will not cause any heap problems in a long run use a 700MB file at least and set your JVM to have only 512MB of heap :

	export MAVEN_OPTS="-Xmx512m"


To run the project you can execute the following Maven goal

    mvn camel:run
    
    
To test it you can place a file in the input folder and name it *.ready
    
    
In order to test with a big file you can

	curl --request PUT  --data-binary @PATH_TO_YOUR_BIG_FILE http://localhost:8123  -v

Or if you prefer post data

	curl --request POST -H "Content-Type: application/octet-stream"  --data-binary @PATH_TO_YOUR_BIG_FILE http://localhost:8123  -v