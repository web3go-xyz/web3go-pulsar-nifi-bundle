# Apache NiFi - Processor for Apache Pulsar

## How to build

This processor allows you to define the versions of the Apache NiFi and Apache Pulsar libraries that you that you want to use inside the processor, along with the JDK version you want to compile the classes with. 

To build the NAR files using Maven, just run the following command:

`mvn clean package -Dnifi.version=<NIFI VERSION> -Dpulsar.version=<PULSAR VERSION> -Djdk.release=<JAVA VERSION>`
 
```dependency check
mvn dependency:tree
```

``` build nar
mvn clean package -DskipTests -Dnifi.version=1.17.0 -Dpulsar.version=2.10.1
```


 

## How to test

A Dockerfile has been included in the project that can be used to test the Processor locally, and can be built using the following command:

`docker build -t <TAG> .`

Currently this command will load NAR files that were build using the default NiFi, Pulsar, and Java versions into the lib folder of the NiFi container for testing. Therefore, if you need to test artifacts built using a different version of these libraries, then you will first need to copy those NAR artifacts into the docker/lib folder *BEFORE* building the Docker image.


## How to use in NiFi

- stop NiFi
- place *.nar to "lib" directory.
- start NiFi

## example
- create new Processor: PublishPulsarRecord
- config:
```
Record Reader:              JsonTreeReader
Record Writer:              JsonRecordSetWriter
Pulsar Client Service:      StandardPulsarClientService
Topic Name:                 persistent://public/web3go/simple-test
Async Enabled:              false
Maximum Async Requests:     50
Batching Enabled:           true
Batching Max Messages:      1000
Batch Interval:             100 ms
Block if Message Queue Full: true
Compression Type:           None
Message Routing Mode:       Round Robin Partition
```

```DetailsStandardPulsarClientService 1.17.0
Pulsar Service URL:         pulsar://172.31.20.253:6650
```