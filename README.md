

# THE COMPLETE USER GUIDE OF THE GETDETAILS END-POINT PERFORMANCE TESTING PROJECT

## 

## **Purpose**

_To guide the reader through the steps needed to follow for review and run the performance test project for the below application._





## **The Application**

[https://api.tmsandbox.co.nz/v1/Categories/<<categoryId>>/Details.json?catalogue=false](https://api.tmsandbox.co.nz/v1/Categories/%3c%3ccategoryId%3e%3e/Details.json?catalogue=false)




## **The folder structure.**

The project was completed based on the Windows OS platform. The folder “**_Assurity_GetDetailsPerf_Artifacts_To_Share”_** is shared, which contains the Other artifacts and screen shots sub folders




### Other Artifacts

**ClickmetoConnect_MithilaJmeterLoadGen** – Please click this rdp file to log in to the AWS server


## **Screen Shots**

This folder contains the useful screen-shots to be referred when necessary.






## **Steps to execute the Performance Test**

 1. Double-click on **ClickmetoConnect_MithilaJmeterLoadGen** remote desktop connection file and you will be navigated to the AWS Windows Load Generator Instance.
 2. The latest code in the GitHub (url given below) has been checked in to the below local repository in the AWS Server: **C:\AssurityGetDetailsPerf\GetDetails_Assurity**
 3. Navigate to the **C:\AssurityGetDetailsPerf\GetDetails_Assurity** location from the command line and execute the below command.

*C:\AssurityGetDetailsPerf\apache-jmeter-5.5\bin\jmeter -Jthreads=5 -JrampUp=5 -Jduration=60 -n -t Assurity_GetDetails.jmx -l result.jtl*
 4.  If you want to change the runtime parameters of the execution please follow the below steps
	 * To change number of threads , modify value to desired value of Jthreads
	 * To change ramp up time , modify value to desired value of -JrampUp
	 * To change duration , modify value to desired value of -Jduration 
5.  The result file(results.jtl) and the csv(*Assurity_ResultsDetailsCSV.csv*) file to which the test writes the CategoryID, Name, Path, Promotional IDs and Prices are generated in this location after the execution **C:\AssurityGetDetailsPerf\GetDetails_Assurity**

 

## The CI integration Jenkins & Grafana

 1. Open a Google Chrome browser and navigate to the Jenkins CI dashboard of the performance test project. Please note that the URL has been given below _[ This Jenkins CI dashboard is publicly accessible]
 2. Click on “**_GetDetails_Assurity”_**  Jenkins job and then click on the “**Build Now**” button in the left navigation.
 3. Once the build is successfully completed, please navigate to the Grafana dashboard using the Grafana url given below and there you can find the below information of the test execution.
		 * Total Requests
		 * Failed Requests
		 * Error Rate %
		 * Transaction Response Times(90th pct)

And some other metrics that will be useful for the analysis.


**Jenkins CI Dashboard**
|URL| Credentials  |
|--|--|
|http:13.54.245.166:8080 | Username : admin     , Password : @dm!N#123|


**Monitoring through Grafana Dashboard**
|URL|  Credentials  |
|--|--|
|http://13.54.245.166:3000/ |  Username : admin, Password: Gr@Fan@|









# Performance Test Report for GetDetails End-Point Performance Testing

**Executive Summary**


**Objective**
To evaluate the GetDetails api performance in terms of the responsiveness and the stability in sustaining in the below mentioned non-functional requirements for the api.

 - Number of concurrent threads should be 5
 - The vUsers should be gradually increased at a rate of 1 user per second to the system.
 - During the steady-state the test should send 10 api calls to the system.
 - The 90th percentile response time should be less than 500 ms

**Test Results and Observations**

1. 3 test iterations of the test were conducted.
2. The below  contains the non functional requirements related to the test execution
**Application** : https://api.tmsandbox.co.nz/v1/Categories/6327/Details.json?catalogue=false

|**User Load**| **Duration** | **Response time SLA**** |
|------------|-------------|---------------------------|
|          5 						| 60 seconds |500 miliseconds

** 90th percentile

**User Load** : 5

**Duration**            : 60 seconds

**90th percentile(pct) Response time SLA** : 500ms

3.  Response times 

|Execution round|  90th pct Response time(ms)|
|---------------------------------------------|--|
|  1                                           |159.3  |
|2|137.3
|3|51.6

During the 1st and 2nd execution rounds, response times of the each first request has been reported respectively **159.3** ms and 148 ms. This has been resulted in higher 90th percentile response time value for those executions. Yet, all iterations results are within the specified response time SLA of 500ms.

4. The category id 6331, does not return the expected values. Therefore, according to the text assertion there is a 10% error rate recorded.

Assumptions
1. The application server (environment on which api is hosted) performance has been considered out-of-scope
2. The loadgenerator environment has been selected AsiaPacific(Sydney) in AWS





