# Universal-DDI-API-JAVA-SDK
# Universal DDI SDK

## Overview

The Universal DDI SDK (Dynamic DNS and IP Address Management SDK) is a Java-based software development kit designed to simplify integration with Dynamic DNS and IP Address Management (IPAM) services. This SDK provides a set of APIs for interacting with DDI services such as DNS, DHCP, and IP address management.

This document outlines the installation and usage of the SDK, including how to integrate it into your Java projects and call its API methods.



---
Table of Contents:

1. Installation Instructions
      Prerequisites
      Installing the SDK via Maven
2. API Reference
      ApiException
      DataCreateRecordResponse
      DataListRecordResponse
      DataReadRecordResponse
      DataRecord
      DataSOASerialIncrementRequest
      DataSOASerialIncrementResponse
      DataUpdateRecordResponse

   

## 1. Installation Instructions

### 1.1 Prerequisites
- **Java 8 or later** is required to use this SDK.
- A **Maven**-based project.
- A **GitHub account** for accessing the private GitHub Maven repository.

### 1.2 Installing the SDK via Maven

To use this SDK, you first need to add it to your project dependencies. The SDK is hosted on GitHub Packages and can be integrated into your project via Maven.

#### Step-by-Step Installation:

1. **Add the GitHub Packages repository to your `pom.xml`**:
   Add the following snippet to the `repositories` section of your `pom.xml`. This will allow Maven to access the GitHub Packages repository:
   
   ```xml
   <repositories>
     <repository>
       <id>github</id>
       <url>https://maven.pkg.github.com/hgupta-infoblox/Universal-DDI-API-JAVA-SDK</url>
     </repository>
   </repositories>
   ```

2. Add the dependency to your pom.xml: Add the following dependency under the <dependencies> section of your pom.xml. Make sure to use the correct version number (for example, 1.0-SNAPSHOT or 1.0.0).

   ```xml
   <dependencies>
     <dependency>
       <groupId>com.info.ddi</groupId>
       <artifactId>ddi-sdk</artifactId>
       <version>1.0-SNAPSHOT</version>  <!-- Update this version as needed -->
     </dependency>
   </dependencies>
   ```

3. Authentication (GitHub Token): To access the private repository, you need to authenticate with your GitHub credentials. If you are using GitHub Packages for Maven, authenticate by adding your GitHub personal access token to your settings.xml file, which is located in the .m2 directory of your Maven installation.

   Example: settings.xml:

         <settings>
           <servers>
             <server>
               <id>github</id>
               <username>your-github-username</username>
               <password>your-github-token</password>
             </server>
           </servers>
         </settings>
   
   Replace your-github-username and your-github-token with your actual GitHub username and token.

1.3 Install the Dependency
    Once the pom.xml is updated, run the following Maven command to download the SDK dependency and install it:

       > mvn clean install

   This will download the SDK from GitHub Packages into your local Maven repository.


--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 3. API Reference
   
  3.1 ApiException
      Description: This class is used to represent an exception or error that occurs during an API call.
    Usage:
    Catch ApiException to handle errors when calling methods like createDnsRecord() or getDnsRecords().
    Example:
   
            try {
                DDIClient client = new DDIClient("apiKey", "apiSecret", "https://api.ddi-service.com");
                client.createDnsRecord("example.com", "A", "192.168.1.1");
            } catch (ApiException e) {
                System.out.println("API Error: " + e.getMessage());
            }
   
  3.2 DataCreateRecordResponse
      Description: Represents the response when creating a new DNS record.
    Fields:
    status: Indicates whether the record was successfully created.
    message: A message providing more details about the result.
    Example:
   
            DataCreateRecordResponse response = client.createDnsRecord("example.com", "A", "192.168.1.1");
            if (response.getStatus().equals("success")) {
                System.out.println("Record created successfully.");
            }
            
  3.3 DataListRecordResponse
      Description: Represents a response that contains a list of DNS records.
      Fields:
      records: A list of DataRecord objects.
      Example:
   
              DataListRecordResponse response = client.getDnsRecords("example.com");
              for (DataRecord record : response.getRecords()) {
                  System.out.println(record.getType() + ": " + record.getValue());
              }
              
  3.4 DataReadRecordResponse
      Description: Represents the response when reading a specific DNS record.
      Fields:
      record: A single DataRecord object containing the details of the requested DNS record.
      Example:
      
              DataReadRecordResponse response = client.readDnsRecord("example.com", "A");
              System.out.println("Record Type: " + response.getRecord().getType());
              
  3.5 DataRecord
      Description: Represents a DNS record (e.g., A, CNAME, MX record).
      Fields:
      type: The type of DNS record (e.g., A, CNAME).
      value: The value associated with the DNS record (e.g., an IP address for A records).
      Example:

              DataRecord record = new DataRecord();
              record.setType("A");
              record.setValue("192.168.1.1");
              
  3.6 DataSOASerialIncrementRequest
      Description: Represents a request to increment the serial number of the SOA record for a zone.
      Fields:
      zoneName: The name of the DNS zone whose SOA serial is to be incremented.
      Example:

              DataSOASerialIncrementRequest request = new DataSOASerialIncrementRequest();
              request.setZoneName("example.com");
              
  3.7 DataSOASerialIncrementResponse
      Description: Represents the response after incrementing the SOA serial number.
      Fields:
      newSerial: The new serial number after the increment.
      Example:

              DataSOASerialIncrementResponse response = client.incrementSOASerial("example.com");
              System.out.println("New SOA Serial: " + response.getNewSerial());
              
  3.8 DataUpdateRecordResponse
      Description: Represents the response after updating an existing DNS record.
      Fields:
      status: Indicates whether the update was successful.
      message: A message providing additional information about the update.
      Example:
              
              DataUpdateRecordResponse response = client.updateDnsRecord("example.com", "A", "192.168.1.1", "192.168.1.2");
              if (response.getStatus().equals("success")) {
                  System.out.println("Record updated successfully.");
              }
