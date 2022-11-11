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