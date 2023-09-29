# 5. Совершение операции перевода

## 5.1 Выполнение операции перевода A2C (Mastercard)

|                  | Value                                                        |
| ---------------- | ------------------------------------------------------------ |
| **HTTPS Method** | POST                                                         |
| **Endpoint**     | <span style="color:red">{{Base URL}}</span>/api/Transfers    |
| **Headers**      | TPS_API_KEY - Ключ аутентификации,<br />TPS_API_REQUEST_ID - ID запроса (numeric)<br />TPS_API_SIGN - подпись аутентификации |

**Описание:**
Система TPS позволяет авторизованному пользователю, в разрезе партнера с соответствующей лицензией, инициировать перевод, что позволяет партнёру осуществлять переводы между различными финансовыми учреждениями. 
reg_date - указывает дату регистрации перевода в системе TPS в формате YYYY-MM-DDTHH:mm:ss.
сonfirm_date - указывает дату подтверждения успешности перевода в TPS YYYY-MM-DDTHH:mm:ss.  


**Параметры запроса:**  
<span style="color:red">Все представленные поля обязательны!</span>

| Key                 | Value                                                                                                                    | Type   | Length |
|---------------------|--------------------------------------------------------------------------------------------------------------------------|--------|--------|
| code                | mastercard_a2c_md<br><br>Все доступные значения возвращает <br>GetAllServices (см. П.10 - Получение доступных сервисов). | String | 1-128  |
| amount              | Сумма получения (в монетах). (Eg. 50000 = 500.00)<br><br>From 1 to 1000000                                               | Long   | -      |
| currency_code       | Код валюты отправления ISO 4217  (Eg. MDL)                                                                               | String | 3      |
| description         | Произвольное описание перевода                                                                                           | String | 1-256  |
| receiver_pan        | Номер карты получателя                                                                                                   | String | 16     |
| receiver_first_name | Имя получателя                                                                                                           | String | 1-64   |
| sender_first_name   | Имя отправителя                                                                                                          | String | 1-64   |
| sender_last_name    | Фамилия отправителя                                                                                                      | String | 1-64   |
| sender_adress       | Адрес отправителя                                                                                                        | String | 1-256  |
| sender_country      | Код страны отправления  (ISO 3166-1 alpha-3)                                                                             | String | 3      |
| sender_country      | Sender’s country code (ISO 3166-1 alpha-3)                                                                               | String | 3      |
| receiver_country    | Код страны получения  (ISO 3166-1 alpha-3)                                                                               | String | 3      |

 > Параметры полей возвращает GetServiceInfoByCode (см. П.11 Получение списка параметров сервиса )

**Request**

```json
{
    "code":"mastercard_a2c_md",
    "amount": 10000,
    "currency_code":"MDL",
    "parameters":
        {
            "description":"Pentru servicii",
            "receiver_pan":"5101882609647449",
            "receiver_first_name":"TestFirst",
            "receiver_last_name":"TestLast",
            "sender_first_name":"Tolgahan",
            "sender_last_name":"COLPN",
            "sender_address":"Chisinau str Bogdan-Voievod 22 ap 27",
            "sender_country":"MDA",
            "receiver_country":"MDA"
        }  
  }
```

**Response: Success - <span style="color:green">200 OK</span>**  
```json
{
    "reg_date": "2023-06-28T08:52:36",
    "confirm_date": "",
    "amount": 10000,
    "currency_code": "MDL",
    "name": "Mastercard transfer to card",
    "code": "mastercard_a2c_md",
    "clearing_amount": 10415,
    "clearing_currency": "MDL",
    "status": "process",
    "transfer_key": "df3311a0-4517-ee11-8b90-00155d325a01",
    "external_id": 1687931555,
    "parameters": 
        {
            "description": "Pentru servicii",
            "receiver_pan": "510188******7449",
            "receiver_first_name": "TestFirst",
            "receiver_last_name": "TestLast",
            "sender_first_name": "Tolgahan",
            "sender_last_name": "COLPN",
            "sender_address": "Chisinau str Bogdan-Voievod 22 ap 27",
            "sender_country": "MDA",
            "receiver_country": "MDA"
        }  
}

```

**Параметры ответа:**  

| Key                 | Value                                                                                                                                                           | Type      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| reg_date            | Дата регистрации транзакции в формате 2023-04-11T08:40:53                                                                                                       | Timestamp |
| confirm_date        | Дата конфирмации транзакции (так как получить конфирмацию сразу же затруднительно, то значение этого поля может быть нулевым).<br>В формате 2023-04-11T08:40:54 | Timestamp |
| amount              | Сумма получения.Указывается в монетах (Eg. 50000 = 500,00)                                                                                                      | Long      |
| currency_code       | Код валюты получения. ISO 4217  (Eg. MDL)                                                                                                                       | String    |
| name                | Наименование сервиса. (Eg. Mastercard transfer to card)                                                                                                         | String    |
| code                | Код сервиса. Eg. mastercard_a2c_md                                                                                                                              | String    |
| clearing_amount     | Clearing amount (см. п.3. Баланс). Указан в монетах (Eg.  55000 = 550.00).                                                                                      | String    |
| clearing_currency   | Код валюты баланса партнера. ISO 4217  (Eg. MDL).                                                                                                               | String    |
| status              | Статус транзакции: confirmed, process, failed                                                                                                                   | String    |
| transfer_key        | Уникальный номер(ключ) транзакции в системе                                                                                                                     | String    |
| external_id         | Уникальный номер транзакции в системе партнера  (TPS_API_REQUEST_ID)                                                                                            | String    |
| description         | Произвольное описание перевода                                                                                                                                  | String    |
| receiver_pan        | Номер карты получателя                                                                                                                                          | Int       |
| receiver_first_name | Имя получателя                                                                                                                                                  | String    |
| receiver_last_name  | Фамилия получателя                                                                                                                                              | String    |
| sender_first_name   | Имя отправителя                                                                                                                                                 | String    |
| sender_last_name    | Фамилия отправителя                                                                                                                                             | String    |
| sender_address      | Адрес отправителя                                                                                                                                               | String    |
| sender_country      | Код страны резидентства отправления (ISO 3166-1 alpha-3)                                                                                                        | String    |
| receiver_country    | Код страны резидентства получения (ISO 3166-1 alpha-3)                                                                                                          | String    |

**400 - Bad request**
```json
{
   "data": null,
   "msg": "BANK_FAILED_REQUEST",
   "code": 353
}
```

