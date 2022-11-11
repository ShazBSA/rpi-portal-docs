# API interface for AVS & RTC

## Account Verification Service

This Verification Service API Documentation describes the flows and payloads used by BankservAfrica in order to verify account information.

The Verification Service will verify the accuracy or validity of any information sent in the request message.

The API endpoints described here will allow a participant to:

+ Verify customer account and identification details, this may include name, ID number, mobile number, bank account details and status of account as well as email address. (Possible verification of address not currently included). This will provide and interface to the existing Account Verification Service (AVS) currently provided by BankservAfrica.  
+ Perform a health check to determine the status of the Verification Service.

## RTC Service

This RTC Service API Specification describes the API flows and payloads used by BankservAfrica in order to process a real-time credit transfer.

The Real Time Credit’s system (RTC) comprises of two legs, the first leg being a non-financial leg which checks the validity of an account prior to the processing of the credit transfer, while the second leg in the process performs the actual real time credit transfer.

The endpoints described here will allow a participant to:
+ Perform a validation check on an account prior to processing a real-time credit transfer, similar to the existing non-financial leg in RTC currently, and
+ Process a real time credit transfer transaction between themselves as the debtor bank and the creditor

This service is similar to the existing RTC system currently provided by BankservAfrica – and may be used in conjunction with or instead of the current RTC system.

### Using the API

Browse the reference section of this site to see examples of what you can do with this API and how to use it. You can use the **Try this API** tool on the right side of an API method page to generate a sample request.

### Design Principles

All APIs are designed to be asynchronous. The sender of the message will receive a synchronous HTTP response to their request, but the verification response message will be asynchronous.  
This makes the API calls more efficient as queues do not need to be maintained and the sender of the message does not need to wait for a response, this also reduces the need to cater for timeouts and subsequent re-tries.

### Standards

Where possible, field names and sizes within the payload have been aligned to ISO20022. In certain instances field lengths have been adjusted in order to ensure compatibility with ISO8583.

### Version Control

The API version will be contained in the corresponding Swagger documentation and will be reflected in the path of the API call eg. /**v1**/creditorVerificationRequest/{instructingAgent}
API versioning will be as follows:  

| Version name | Implementation description  |  
| ------------ | ----------------------------|
| v1alpha      | Initial alpha version, this version is subject to change without notification |
| v1beta  | Initial beta version, this version may be changed based on input from external participants (banks). Changes will first be communicated to all involved parties, before being applied |  
| v1.0 - major version | Major versions will be indicated by the integer portion of the version number. Major version numbers will begin at 1 and increment by 1 for each subsequent version. A new major version will be released for changes such as a new message or message name change. |
| v1.1 - subversion | Minor versions will be indicated by the value as contained after the decimal point in the version number. Minor version changes will be of such a nature that both newer versions and older versions can be handled by , this means that changes will most likely only be the addition or deprecation of fields within the payload.
| |NOTE: In order to facilitate the support for different minor versions the minor version number will be contained in the payload and not in the URI.

Depending on the nature of the change from one major version to another, it may or may not be possible to support multiple versions. Should multiple versions be supported, the older version will only be supported for a maximum of 3 months post implementation of the new version.

Details of any notable changes can be found in the Changelog

## Link to swagger

[AVSswagger.json](http://dev-avs.endpoints.bsarpi.cloud.goog/v1beta1/verification/swagger.json)

[AVSBswagger.json](http://dev-avs.endpoints.bsarpi.cloud.goog/v1alpha1/avsb/swagger.json)
