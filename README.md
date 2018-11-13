# Junior Data Engineer Assignment
Assignment for junior data engineer position

## Introduction
Chama is a company that exposes itself through an IOS and Android App. The success or insuccess of the company is thightly related to how the App performs. How it is able to keep users engaged and get to the end of the purchase flow.

-----

### Exercice 1: Device Uninstalls
The Chama App reports uses the Firebase SDK to report events. In the firebase event information it's possible to find DeviceId's and InstanceId's. 
 - DeviceId is relative to the physical device, the phone or tablet where the application is installed.
 - InstanceId is a code given everytime that the device installs the application. Meaning, if the same device installs the App several times, will gain new instanceId's but the deviceId will remain the same.

Every event has the DeviceId, but due technical reasons, the uninstall event, only has deviceId information. 

#### the problem:
There's a strong need to determine which instance belongs to what uninstall event, so that is possible to determine how long was the App installed.

*Uninstall event information*

|DeviceId|EventName|EventDateTime|
|---|---|
|DeviceA|uninstall|Dec 4, 2018 10:45:00|
|DeviceB|uninstall|Dec 5, 2018 11:45:00|
|DeviceC|uninstall|Dec 6, 2017 12:45:00|


*Instance information*

|Instance|DeviceId|InstanceFirstSeenDateTime|
|---|---|
|InstanceA1|DeviceA|Nov 1, 2018 13:45:00|
|InstanceA2|DeviceA|Dec 2, 2018 14:45:00|
|InstanceB1|DeviceB|Nov 1, 2018 15:45:00|
|InstanceB2|DeviceB|Dec 4, 2018 16:45:00|
|InstanceCX|DeviceC|Dec 4, 2018 00:00:00|


The goal here is to create a enriched, and clean Uninstalls table in some database so that other people can query this information. **Please answer the following**:
 - Imagine that this last 2 tables have more than a million rows each, in order to create the final Uninstall table, how would you proceed?
 - As you noticed, the date format in the tables is not the best to be parsed into a datetime column, how can you surpass this issue?
 - The DeviceC as uninstall date prior to what we see in [InstanceFirstSeenDateTime].
   - What could be the cause of such situation?
   - Would you include DeviceC in the final Uninstalls table? Why? If it "depends", please elaborate your awnser.
 - When you read the words "enriched" and "clean" in the premisse of the problem, what was your understanding of them?
 - Should a data engineer be responsible to integrity of the data? Why? Also, please, write in a sentence your understanding of the word "integrity" in the role of data engineer.

Desired final table:

|Instance|DeviceId|EventName|InstanceFirstSeenDateTime|EventDateTime|
|---|---|---|
|InstanceA2|DeviceA|uninstall|Dec 2, 2018 14:45:00|Dec 4, 2018 10:45:00|
|InstanceB2|DeviceB|uninstall|Dec 4, 2018 16:45:00|Dec 5, 2018 11:45:00|

(DeviceC is up to you to include it or not)

**Please present a working solution for this problem starting with the [Instances.csv](Instances.csv) and [UninstallEvents.csv](UninstallEvents.csv) files.**

-----

### Exercice 2: External integration
An external provider wants to send us information about popular opinion about Chama company and App. They offer two options to send the information. 
One option is to POST the information, in a URL endpoint that we own, everytime that something happens, near real time.
The second option is for us to download information in bulk, CSV format, once a day. 
**Please answer the following**:
 - What option would you choose? Please elaborate your awnser.
 - What are the advantages of each scenario?

Using draw.io or similar, please design a detailed flow that describes the option that you preferred. Please mention the technologies that you would choose for the different steps.
