# Enumerations

The following tables show the possible enumeration values catered for in the verification service.

## Member Identifiers 

These are the agent identifiers

Bank Name | Institution Identifier | File literal
--- | --- | ---
ABSA Bank | 210016 | T0
African Bank | 210007  | AN
Albaraka Bank | 210052  | LB
Bank of Windhoek | 210014 | R0
Bidvest Bank | 210044 | R1
Capitec Bank | 210010 | N0
Citibank |210033 | AG
Discovery Bank | 210063 | DB
Finbond Mutual Bank | 210055 | FM
FirstRand Bank | 210003 | A0
Grindrod Bank |210047 | GL
Grobank | 210006 | H0
HBZ Bank Limited | 210036 | AJ
Investec Bank | 210039 | AM
Ithala Bank | 210030 | AD
Mercantile Bank  |210009 | J0
Nedbank | 210002 | D0
South African Post Office (SAPO) | 210013 | A0
SASFIN Bank | 210058 | S5
Standard Bank of South Africa (SBSA) | 210001 | B0
Standard Charter Bank | 210042 | AQ
Tyme Digital | 210061 | CW
UBank | 210019 | X0

## Account Type

These indicate the type of account

ISO8583 Code | Description | ISO20022 Code | Description
------------ | ---------- | ------------- | -----------
00 | No account specified | OTHR | Other - not specified
01 | Cheque account type |CACC | Current
02 | Savings account type | SVGS | Savings
03 | Transmission account | TRAN | Transactional
04 | Bond account  | LOAN | Loan:Bond  
06 | Subscription share | TRAS | Share trading

## Verification Response Codes

The table below details the possible ISO20022 External Verification Reason Codes to be used in the verification response message.

|Code | Name | AVS/RTC
---- | ---------- | ----
0000 | VerificationSuccessful | 00
AB07 | Offline Agent(Bank offline) | 91
AB05 | Timeout Creditor Agent | 68
AG01 | Transaction Forbidden | 05
AG03 | Transaction Not supported | 12
DT01 | Invalid Date | Q0
FF02 | Syntax Error | 06
FF10 | Bank System Processing Error | 96
RC02 | Invalid Bank Identifier | 31
TD03 | Incorrect File structure(insufficient detail) | 30

## Private Identification Type

These following ISO20022 codes are used to indicate the type of identification to be verified

Type | Description
------------- | -----------
NIDN | National Identity Number
CCPT | Passport

## HTTP Response Codes

The following default HTTP response codes will be used in the HTTP response messages

Code | Description | gRPC response | Detailed description
----| -----------| -------------| --------
200 | A successful response. | OK | Transaction accepted
400 | Bad request. | INVALID_ARGUMENT | The contents of the message were invalid
404 | Resource does not exist. | NOT_FOUND | Endpoint invalid or not found
412 | Precondition Failed. | FAILED_PRECONDITION | Payload content failed basic validation, message rejected
500 | Internal Server Error.

## Status Codes

Code | Description
---- | ----------
ACCP | Accepted
RJCT | Rejected
