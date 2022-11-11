# Examples

## AVS Realtime

The Verification Service serves as an interface to the BankservAfrica AVS-R system to verify  account information  

Example payloads are shown below:

## Verification of account information
  
To validate account information using AVS the following minimal information must be provided in the request.  

In the example below, instructing bank 210005 sends a request to validate the customer's ID number, bank account and e-mail address provided.  

POST /verification/request/210005

```json
{
  "uetr": "c932ad8a-b6fe-4f8e-bfa1-2a9864bcd381",
  "creation_date_time": "2019-07-04T15:11:00.00000",
  "reference": "2a9864bcd381",
  "account": "87456123",  
  "private_identification": "8405050069088",
  "private_identification_type": "NIDN",
  "branch_identification": "721234",
  "creditor_agent": "210004",
  "email_address": "somebody@somewhere.com",
  "debtor_agent": "210005",
  "check_credits_allowed": true,
  "check_debits_allowed": true,
  "check_older_than_three_months": true
}
```

If the above details are valid, the response message from the receiving bank(the creditor in this example) will look as follows:

POST /verification/response/210004  

```json
{
  "uetr": "c932ad8a-b6fe-4f8e-bfa1-2a9864bcd381",
  "creation_date_time": "2019-07-04T15:11:30.00000",
  "reference": "2a9864bcd381",
  "account": "87456123",  
  "private_identification": "8405050069088",  
  "private_identification_type": "NIDN",
  "branch_identification": "721234",
  "creditor_agent": "210004",
  "email_address": "somebody@somewhere.com",
  "debtor_agent": "210005",
  "response_code": "0000",
  "account_found": "Y",
  "account_open": "Y",
  "account_type_match": "Y",
  "mobile_match": "Y",
  "credits_allowed": "Y",
  "debits_allowed": "Y",
  "email_match": "Y",
  "private_identification_match": "Y",
  "initials_match": "Y",
  "name_match": "Y",
  "older_than_three_months": "Y"
}
```

For a list of possible response codes that may be returned see the Enumerations page.

Should, for example, the email details not match those as held by the receiving bank, and the account not be open the account_open and email_match parameter will be returned as false.  

```json
{
  "uetr": "c932ad8a-b6fe-4f8e-bfa1-2a9864bcd381",
  "creation_date_time": "2019-07-04T15:11:30.00000",
  "reference": "2a9864bcd381",
  "account": "87456123",  
  "private_identification": "8405050069088",  
  "private_identification_type": "NIDN",
  "branch_identificationgit ": "721234",
  "creditor_agent": "210004",
  "email_address": "somebody@somewhere.com",
  "debtor_agent": "210005",
  "response_code": "0000",
  "account_found": "Y",
  "account_open": "N",
  "account_type_match": "Y",
  "mobile_match": "Y",
  "credits_allowed": "Y",
  "debits_allowed": "Y",
  "email_match": "N",
  "private_identification_match": "Y",
  "initials_match": "Y",
  "name_match": "Y",
  "older_than_three_months": "U"
}
```  

# AVS Batch
 
The AVS Batch system allows for a group (batch) of transactions to be sent for validation.  
The sending bank will send a batch of records to be validated, BankservAfrica then split the incoming batch into files (or API messages) for validation at each of the different receiving banks.  

The example below shows a BBxx001D file and its corresponding AVS Batch API message.

## Examples

### Batch Request

![AVS Batch Request Flow Diagram](/images/AVS_Batch-Request.png)

BBB0001D  

```
0120201020AVS TO VERIFY 0001ACBJBBB0001D0001DATAOUT20201020TEST06000000        091143
02000000120201020TEST
14000000204000000520201020TEST210007DSB20201020         9000009076321000105100100000000000000000112306817609295639083O    MOTSAGE                                                     OPENYYY                                                                                                                     YYYYYNBAAN001D
14000000304000000620201020TEST210007DSB20201020         9000015521021000105100100000000000000028609891128211036020084LG   KLEYNHANS                                                   OPENYYY                                                                                                                     YYYYYNBAAN001D
980000004TEST000000000000020000000000000040000000010
9920201020AVS TO VERIFY 00010000060000999900000000000000000000000000000000000000000000
 ```  

 POST /v1alpha1/avsb/request   

 ```json
 {
  "header": {
    "messageIdentification": "20201020-BBB0001D-001/001",
    "creationDateTime": "2020-10-20T09:38:12.002312",
    "numberOfTransactions": 2
  },
  "messages": [
    {
      "instructingAgent": "210007",
      "uetr": "b9e73a9c-2ce6-49fe-814d-15dd85adb665",
      "creationDateTime": "2020-10-20T09:38:15.003471",
      "reference": "DSB20201020         90000090763",
      "instructedAgent": "210001",
      "branchIdentification": "051001",
      "account": "1123068",
      "accountType": "CACC",
      "privateIdentification": "7609295639083",
      "privateIdentificationType": "NIDN",
      "initials": "O",
      "name": "MOTSAGE",
      "checkDebitsAllowed": true,
      "checkCreditsAllowed": true,
      "checkOlderThanThreeMonths": true
    },
    {
      "instructingAgent": "210007",
      "uetr": "945760f2-dcb6-406f-94b1-895fafdc864a",
      "creationDateTime": "2020-10-20T09:38:18.003471",
      "reference": "DSB20201020         90000155210",
      "instructedAgent": "210001",
      "branchIdentification": "051001",
      "account": "286098911",
      "accountType": "SVGS",
      "privateIdentification": "8211036020084",
      "privateIdentificationType": "NIDN",
      "initials": "LG",
      "name": "KLEYNHANS",
      "checkDebitsAllowed": true,
      "checkCreditsAllowed": true,
      "checkOlderThanThreeMonths": true
    }
  ]
}
```  



