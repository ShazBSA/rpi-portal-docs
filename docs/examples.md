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
````

