# Centrify External Credential Storage Integration

### Introduction

External Credential Storage is a good mechanism for storing credentials that employees share to access web service.
The audit log mechanism of such solution lets you also know what credential an employee accessed.

Centrify Vault Suite reduces the complexities associated with securing and sharing access to privileged accounts.
Continuous discovery of systems and automated enrollment in the Centrify Platform ensures privileged access governance
where shared account credentials are either vaulted or eliminated.
A ServiceNow instance can store credentials used by Discovery, Orchestration,
and Service Mapping in such external credential repository rather than directly in a ServiceNow credentials record.

### Prerequisite

#### 1. Download the Centrify Credential Resolver JAR File, To download the plugin.
     navigate to the Centrify Download Center: www.Centrify.com > Support > Downloads and click on the Tools and Plugins > ServiceNow Integration.

#### 2. Activate the External Credential Plugin on ServiceNow Instance.
Reference :- https://docs.servicenow.com/bundle/paris-servicenow-platform/page/product/credentials/task/t_ActivateExtrnlCredStoragePlugIn.html

#### 3.  Activate the Discovery plugin on ServiceNow Instance.
Reference :- https://community.servicenow.com/community?id=community_question&sys_id=67f8cd5fdb1e9414fa192183ca961936

#### 4.  Download Mid Server from ServiceNow Instance.
Reference :- https://docs.servicenow.com/bundle/rome-servicenow-platform/page/product/mid-server/task/t_DownloadMIDServerFiles.html

#### 5.  Install Mid server
Reference :- https://docs.servicenow.com/bundle/rome-servicenow-platform/page/product/mid-server/concept/mid-server-installation.html

#### 6. Validate the Mid Server
Reference :- https://docs.servicenow.com/bundle/rome-servicenow-platform/page/product/mid-server/task/t_ValidateAMIDServer.html#t_ValidateAMIDServer


> Note: Vault Suite 21.5 specific setup for Domain Account Access
> ##### 1. Download and Install the Centrify Connector from Centrify Portal.
> ##### 2. Register the connector with Domain and PAS portal.(https://docs.centrify.com/Content/CoreServices/Connector/ConnInstall.htm)
> ##### 3. Verify the connector is correctly configured using the "Test Connection" option on the connector page.
> ##### 4. Verify the domain and account setting on PAS.
> ##### 5. Follow the remaining steps as mentioned in Step 2 under Centrify Vault usage section.

---

### Centrify Vault usage

#### 1. For Local Account of the Server.
        1.1 Enroll/Create the System in Centrify Vault.
        1.2 Add the suitable user in the accounts section for the system.
        1.3 Create an ServiceUser provide all the required rights.
        1.4 Provide the view permission of the system to the ServiceUser.
        1.5 Provide the checkout permission of the system account to the ServiceUser.

#### 2. For Active Directory Account of the Server.
        2.1 Enroll/Create the System in Centrify Vault.
        2.2 Add the suitable active direcotry user in the accounts section for the system.
        2.3 Active Directory username have to support format "domainName/AccountName"
        2.4 Create an ServiceUser provide all the required rights.
        2.5 Provide the view permission of the system to the ServiceUser.
        2.6 Provide the checkout permission of the active directory account to the ServiceUser.

#### 3. For Database Accounts.
        3.1 Enroll/Create the database in Centrify Vault.
        3.2 Add the suitable database user to the database under the accounts section.
        3.3 Create an ServiceUser provide all the required rights.
        3.4 Provide the view permission of the database to the ServiceUser.
        3.5 Provide the checkout permission of the database account to the ServiceUser.

### Usage
#### 1. Upload the JAR File on the ServiceNow instance and Synchronize with Mid Server Instance.
Reference :- https://docs.servicenow.com/bundle/rome-servicenow-platform/page/product/mid-server/task/t_SynchronizeAJARFiletoMIDServers.html

#### 2. Configure the Mid Server config.xml
		2.1 You need to enter the Centrify Tenant related information in the config file of mid server agent.
		2.2 Put the below value in agent config.xml
			<parameter name="basic_auth_str" value="bWlkdXNlckBzZXJ2aWNlbm93LmNvbTpDZW50cmlmeUAxMjM="/>
			<parameter name="host" value="aaq0684.my.centrify-qa.net"/>
			<parameter name="application_id" value="oauthsiem1"/>
			<parameter name="grant_type" value="client_credentials"/>
			<parameter name="scope" value="siem"/> 
			<parameter name="proxy_port" value=""/>
			<parameter name="proxy_host" value=""/>

#### 3. Credential Plugin Test for Windows Local Account
        3.1 Vaulted system in Centrify must follow all the guidelines for local accounts mentioned in the Centrify Vault usage section
        3.2 Create a Windows credential in ServiceNow Instance by Navigate to Discovery > Credentials. 
        3.3 Click New.
        3.4 Select window credential type.
        3.5 Select the External credential store check box.
        3.6 The User name and Password fields disappear, and the Credential ID field appears
        3.7 Enter the unique key configured for external credentials in the JAR file uploaded
        to the MID Server for an external credential system. eg.(Administrator)
        3.8 Click Test Credential
        3.9 Enter the Target Machine IP address/hostname.
        3.10 Choose the Mid Server
        3.11 Click OK, this will test for your unique credentialID with Centrify Credential Resolver file.


#### 4. Credential Plugin Test for Active Directory Domain Accounts
        4.1 Vaulted system in Centrify must follow all the guidelines for Active Directory mentioned in the Centrify Vault usage section.
        4.2 Create a Windows credential in ServiceNow Instance by Navigate to Discovery > Credentials. 
        4.3 Click New.
        4.4 Select window credential type.
        4.5 Select the External credential store check box.
        4.6 The User name and Password fields disappear, and the Credential ID field appears
        4.7 Enter the unique key configured for domain accounts for external credentials in the JAR file uploaded
            to the MID Server for an external credential system eg.(domainname\Administrator)
        4.8 Click Test Credential
        4.9 Enter the Target Machine IP address/hostname.
        4.10 Choose the Mid Server
        4.11 Click OK, this will test for your unique credentialID with Centrify Credential Resolver file.

#### 5. Credential Plugin Test for Database Accounts
        5.1 Vaulted system in Centrify must follow all the guidelines for database accounts mentioned in the Centrify Vault usage section.
        5.2 Create a Database credential in ServiceNow Instance by Navigate to Discovery > Credentials. 
        5.3 Click New.
        5.4 Select JDBC credential type.
        5.5 Select the External credential store check box.
        5.6 The User name and Password fields disappear, and the Credential ID field appears
        5.7 Enter the unique key configured for database accounts for external credentials in the JAR file uploaded
        to the MID Server for an external credential system eg.(databaseusername)
        5.8 Click Test Credential
        5.9 Enter the Target IP address/hostname of the database.
        5.10 Provide an relevant port number.
        5.11 Select the appropriate database type.
        5.12 Provide the database name.
        5.13 Choose the Mid Server
        5.14 Click OK, this will test for your unique credentialID with Centrify Credential Resolver file.
