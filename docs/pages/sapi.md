# Transfer to a bank account using the SAPI system

## Send

|                 |Value                                    |
|-----------------|-----------------------------------------|
|**HTTPS method:**|POST                                     |
|**Endpoint:**    |{{Base URL}}/api/Transfers               |
|**Headers:**     |PS_API_KEY - Authentication key          |
|                 |TPS_API_REQUEST_ID. Request ID (numeric).|
|                 | TPS_API_SIGN - Authentication signature |

</br>

<span style="color:red"> **All fields are mandatory!** </span>

| Key                 | Value                                                                                                             | Type   | Length |
|---------------------|-------------------------------------------------------------------------------------------------------------------|--------|--------|
| code                | bank_account_md_topup                                                                                             | String | 1-128  |
| amount              | Receiving amount (in coins). (Eg. 50000 =<br>500.00).<br>From 1 to 1000000                                        | Long   | -      |
| currency_code       | Sending currency code, ISO 4217, а unique<br>three-letter code to each currency, such as MDL<br>for Moldavian Leu | String | 3      |
| description         | Any description of a transaction                                                                                  | String | 210    |
| receiver_first_name | Receiver’s first name                                                                                             | String | 1-64   |
| receiver_last_name  | Receiver’s last name                                                                                              | String | 1-64   |
| sender_last_name    | Sender’s last name                                                                                                | String | 1-64   |
| sender_first_name   | Sender’s first name                                                                                               | String | 1-64   |
| sender_adress       | Sender’s address                                                                                                  | String | 1-256  |
| receiver_country    | Receiver’s country code (ISO 3166-1 alpha-3)                                                                      | String | 3      |
| sender_country      | Sender’s country code (ISO 3166-1 alpha-3)                                                                        | String | 3      |
| sender_city         | The city from which the funds were sent                                                                           | String | 1-256  |
| receiver_iban       | International Bank Account Number (IBAN) of<br>the beneficiary bank                                               | String | 24     |

## Request

```json
"code":"bank_account_md_topup",
"amount":100000,
"currency_code":"MDL",
"parameters":
            {
                "description":"SAPI Test",
                "sender_first_name":"SendFirstName",
                "sender_last_name":"SendLastName",
                "sender_address":"Chisinau str Decebal 6",
                "sender_country":"MDA",
                "receiver_first_name":"Test",
                "receiver_last_name":"merchant P",
                "receiver_iban": "MD38MO2224ASV50651447100",
                "receiver_idnp": "0960001112223",
                "receiver_country": "MDA",
                "sender_city": "Chisinau"
            }   
```



## Response. Success - <span style="color:green">200 OK</span>


```json
"reg_date": "2023-08-11T14:14:09",
"confirm_date": "",
"amount": 100000,
"currency_code": "MDL",
"name": "A service to topup bank account md",
"code": "bank_account_md_topup",
"clearing_amount": 100000,
"clearing_currency": "MDL",
"status": "process",
"transfer_key": "ff34f92b-3838-ee11-8b90-00155d325a01",
"external_id": 1691752436,
"parameters": 
            {
                "description": "SAPI Test",
                "sender_first_name": "SendFirstName",
                "sender_last_name": "SendLastName",
                "sender_address": "Chisinau str Decebal 6",
                "sender_country": "MDA",
                "receiver_first_name": "Test",
                "receiver_last_name": "merchant P",
                "receiver_iban": "MD38MO2224ASV50651447100",
                "receiver_idnp": "0960001112223",
                "receiver_country": "MDA",
                "sender_city": "Chisinau"
            }
```
