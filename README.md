# Demo - Cisco IOS XE - Postman Collections

This demo contains a POSTMAN environment and collection that can be used to interact with the IOS XE on CSR Latest Code Always On Sandbox. The IOS XE on CSR Latest Code Always On Sandbox offers developers shared, VPNless access to an IOS XE device running the latest IOS XE code release available on cisco.com. Here you can test out the newest programmability features and data models available

The environment is pre-configured to access the IOS XE on CSR Latest Code Always On Sandbox. Postman collection for Cisco IOS XE RESTCONF + YANG Model Driven Programmability interface (API)

You can edit the variables in the environment to point to your own IOS XE device. Feel free to modify them as you see fit and to add more calls to the collection.

Background

RESTCONF stands for the HTTP-based Representational State Transfer Configuration Protocol (RESTCONF). RESTCONF provides a programmatic interface based on standard mechanisms for accessing configuration data, state data, data-model-specific Remote Procedure Call (RPC) operations and events, defined in the YANG model.



This RESTful API allows a computer to interact with networking devices to get information from them and to push information. We also can manage large amount of devices with just a single computer using network automation.

RESTful API uses HTTPS and commands like PUT and GET to send information to and from the Cisco devices.



In this demo you will learn:
* How to enable RESTCONF on a Cisco C9300 switch
* How to create and manipulate the Postman collections

![](imgs/Restconf.png)


### Step 1 : Enable RESTCONF on the device

In your terminal window, telnet to 10.1.1.5.


Enter the following configurations to enable RESTCONF on the switch

```
conf t
ip http secure-server
ip http authentication local
restconf
aaa new-model
aaa authentication login default local
aaa authorization exec default local
aaa session-id common
username admin privilege 15 secret 9 ....
```

#### Prerequisite steps: create Postman Collection

These steps are already done for you!

Navigate to Postman application to create your first Postman Collection

* Click on **"New"**

* In the pop-up window click on **"Collection"**

![](imgs/Postman_Create_Collection.png)

* In the "Collection Name" Bar enter the following name:

**Programmability and Automation**
* Navigate to the **"Authorization"** tab and select **"Type"** from the drop-down - **"Basic Auth"**

* Enter Username and Password

```
Username: admin
Password: Cisco123
```
![](imgs/Postman_Create_a_new_Collection_and_Authorization.png)


1. Navigate to **"Variables"** tab and create the following new variables that we are going to use in this demo
```
      **Variable**      **Initial Value**       **Current Value**
        host              10.1.1.5                10.1.1.5
        username          admin                   admin
        password          Cisco123                Cisco123
```

2. Select **"Create"**

![](imgs/Postman_Collection_Variables.png)

#### Prerequisite step: Create Folder within the Collection

These steps are already done for you!

* Next to the collection that you have created, click on three dots.

* Select **"Add Folder"**

<img src="imgs/Postman_Add_Folder.png" width="700" height="800">
<p></p>

* Create a folder name - **"RESTCONF"**

* Navigate to **"Authorization tab"**
* For the type select **"Inherit auth from parent"**
* Click on **"Create"**


<img src="imgs/Postman_Folder_Settings.png" width="700" height="700">

### Step 4: Create GET/PATCH/POST/DELETE API calls

#### First API Call

* Enter request URL where {{host}} is your variable **10.1.1.5**

  * https://{{host}}/restconf/data/ietf-interfaces:interfaces


* Navigate to **"Authorization"** and select **"Inherit auth from parent"**

![](imgs/Postman_First_API_call.png)

* Navigate to **"Headers"** and enter the following information

* In the Key field enter **"Accept"** and **"Content-Type"**
* In the Value field enter **"application/yang-data+json"** for both field

![](imgs/Postman_Headers.png)

#### Save the first API call

* Click on **"Save"** button

![](imgs/Postman_save.png)

* In the **"Request name"** field enter - **ietf-interfaces:interfaces**

* Select a collection or folder to save to: **"RESTCONF"**
* Click on **"Save to RESTCONF"**

<img src="imgs/Postman_Save_request.png" width="700" height="700">
<p></p>

* Click **"Send"**

You should get the following response:

![](imgs/Postman_request.png)

*Notice the status of the response, it defines the status of the request. In our case, we got status 200 OK, which means that we got a successful request.*

##### Congratulations, you successfully created and saved your first API call!!!


#### Perform the same steps for the following GET requests

<p></p>

**Read entire configuration (same as show running-config)**

https://{{host}}/restconf/data/Cisco-IOS-XE-native:native



**Read all vlans on device**

https://{{host}}/restconf/data/Cisco-IOS-XE-vlan-oper:vlans/vlan



**Send a request to get a single interface**

https://{{host}}/restconf/data/Cisco-IOS-XE-interfaces-oper:interfaces/interface=GigabitEthernet1%2F0%2F14/

https://{{host}}/restconf/data/Cisco-IOS-XE-native:native/interface/GigabitEthernet=1%2F0%2F14/

**Read mac addresses for a specific interface (Read MAC Address Table)**

https://{{host}}/restconf/data/Cisco-IOS-XE-matm-oper:matm-oper-data

**Read all arp entries**

https://{{host}}/restconf/data/Cisco-IOS-XE-arp-oper:arp-data
