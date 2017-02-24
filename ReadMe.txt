large-http-streams
=========================================

This projects shows how you can setup http services with minimal configuration that are able to handle 
large streams of data without encountering memory issues.
It uses the camel-http4 component for sending data and the camel-jetty component to receive.


Blog article for more details about handling large stream will come soon on :
https://alainpham.github.io


To build this project use

    mvn install

To make sure that it will not cause any heap problems in a long run use a 700MB file at least and set your JVM to have only 512MB of heap.
We will see that the file is not loaded entirely into memory but it is streamed.
:

	export MAVEN_OPTS="-Xmx512m"


To run the project you can execute the following Maven goal

    mvn camel:run
    
    
To test for the raw big file routes you can place a file in the input folder and name it *.ready
    

You can also use curl command to send your files

To launch a raw big file

	curl --request PUT  --data-binary @PATH_TO_YOUR_BIG_FILE http://localhost:8123  -v


You can test big CSV files with streaming split tokenizer and Bindy parsing
	1/ Generate a 700MB File : launch class GenerateCSVData
	2/ curl --request PUT  --data-binary @700MB.csv http://localhost:8123/csv  -v
	
You can test big XML files with streaming split xtokenizer
	1/ Generate a 700MB File : launch class GenerateXMLData
	curl --request PUT  --data-binary @700MB.xml http://localhost:8123/xml  -v


Or if you prefer post data

	curl --request POST -H "Content-Type: application/octet-stream"  --data-binary @PATH_TO_YOUR_BIG_FILE http://localhost:8123  -v