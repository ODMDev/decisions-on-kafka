# ODM Decision Server with kafka
[![Build Status](https://travis.ibm.com/MYattara/ODM-DecisionServer-Kafka.svg?token=YUDWXbAcjsyzHsqNF4a8&branch=master)](https://travis.ibm.com/MYattara/ODM-DecisionServer-Kafka)
[![GitHub last commit (branch)](https://img.shields.io/github/last-commit/ODMDev/odm-ondocker/dev.svg)](https://github.ibm.com/MYattara/ODM-DecisionServer-Kafka)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

## Features


This sample show how to use IBM ODM with Kafka

![Sample Architecture](ODM-J2SEclient/docs/images/architecture.png)

### Workflow Description

1. We have n client application which reacte as kafka Producer and send their payload to the kafka topic named Requests

2. We have n Business Application implementing ODM Xu which reate as Consumer and execute the payload.

3. 
## Requirments

* Kafka
* IBM ODM
* Maven


## Dependencies
- Compile time
- Test
## Before starting
* Make sure you have kafka installed, start kafka by launching zookeeper and kafka-server
* Clone the project repository from github.
`$ git clone --branch=master git@github.ibm.com:MYattara/ODM-DecisionServer-J2SE-Kafka.git`
* In the pom file set the property <ibm.odm.install.dir></ibm.odm.install.dir> with your odm installation directory.

## Scenario Deployment

According to the sub-scenario we'll use one or many Client Application sending one or many payload to one or many business Application.
the client Application is a J2SE Applications which sends a payload with information about the Borrower and a Loan Request, and wait for the approval or a reject of his loan request.
The business Application is a J2SE ODM execution server in Memory application, which execute the payload against ODM loan validation sample ruleset and then return a result which should be approved or reject to J2SE Client Application

### Sub-scenario 1 : N Client Applications Sending payload to Business Application and waiting for the result
The goal of this sub-scenario is to show each client Application got the right answer for his payload


* Run the project locally.
`$ mvn clean install -Dmessage="yourMessage" -DtopicName="topicName" -Dserverurl="yourkafkahost:9092" -Dgroupid="ConsumerGroupid"`
* To run the main class SampleMain :$ `mvn exec:java -Dexec.mainClass="odm.ds.kafka.main.SampleMain" -Dexec.args="yourkafkahost:port topicname message" -Dmaven.test.skip=true`
* To run the integration test : `$ mvn -Dtest=SampleTest -Dmessage="yourMessage" -DtopicName="topicName" -Dserverurl="yourkafkahost:port" test`
* To run the Main Application of the J2SEclient Application : 
`$ mvn exec:java -Dexec.mainClass="odm.ds.kafka.odmj2seclient.Main" -Dexec.args="/test_deployment/loan_validation_with_score_and_grade 
'{\"borrower\":{\"lastName\" : \"Yattara\",\"firstName\" : \"John\", \"birthDate\":191977200000,\"SSN\":\"11243344\",\"zipCode\":\"75012\"
,\"creditScore\":200,\"yearlyIncome\":20000},\"loanrequest\":{ \"numberOfMonthlyPayments\" : 48,\"startDate\" : 1540822814178,
\"amount\":100000,\"loanToValue\":1.20}}' 'localhost:9092' 'multipart' 'repliestest' 'test2'" -Dexec.classpathScope="test" 
-Dibm.odm.install.dir="C:\ODM8920"`

* To run the Business Application : `$ mvn exec:java -Dexec.mainClass="odm.ds.kafka.odmj2seclient.BusinessApplication" 
-Dexec.args="/test_deployment/loan_validation_with_score_and_grade 'localhost:9092' 'multipart' 'repliestest' 'test2'" -Dexec.classpathScope="test"
 -Dibm.odm.install.dir="C:\ODM8920" `
 
 * To run the Client Application : `$ mvn exec:java -Dexec.mainClass="odm.ds.kafka.odmj2seclient.ClientApplication" -Dexec.args="'{\"borrower\":{\"lastName\" : 
 \"Yattara\",\"firstName\" : \"John\", \"birthDate\":191977200000,\"SSN\":\"11243344\",\"zipCode\":\"75012\",\"creditScore\":200,
 \"yearlyIncome\":20000},\"loanrequest\":{ \"numberOfMonthlyPayments\" : 48,\"startDate\" : 1540822814178, \"amount\":100000,\"loanToValue\":1.20}}' 'localhost:9092' 
 'multipart' 'repliestest' 'test2'" -Dexec.classpathScope="test"`

### Sub-scenario 2 : N Client Applications Sending payload to n Business Application

The goal of this sub-scenario is to show the loadbalacing between Business Application


### Sub-scenario 3 : Availability after one business Application has been down


## Contributing

## References
* [IBM Operational Decision Manager Developer Center](https://developer.ibm.com/odm/)
* [Java EE rule session](https://www.ibm.com/support/knowledgecenter/en/SSQP76_8.9.2/com.ibm.odm.dserver.rules.samples/res_smp_topics/smp_res_javaee.html)

## Issues and contributions

## License
[Apache 2.0](LICENSE)
## Notice
© Copyright IBM Corporation 2018.

[![Build Status](https://travis.ibm.com/MYattara/ODM-DecisionServer-Kafka.svg?token=YUDWXbAcjsyzHsqNF4a8&branch=master)](https://travis.ibm.com/MYattara/ODM-DecisionServer-Kafka)
[![GitHub last commit (branch)](https://img.shields.io/github/last-commit/ODMDev/odm-ondocker/dev.svg)](https://github.ibm.com/MYattara/ODM-DecisionServer-Kafka)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)

