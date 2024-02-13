# Получение доступных сервисов

**GetAllServices**

| HTTPS Method | GET                                                          |
| ------------ | ------------------------------------------------------------ |
| Endpoint     | <span style="color:red">{{Base URL}}</span>/api/Services                                    |
| Headers      | API_KEY - Ключ аутентификаци, <br />API_REQUEST_ID - ID запроса (numeric),<br />API_SIGN - подпись аутентификации |

**Описание:**

Запрос позволяет получить список доступных сервисов для осуществления денежных переводов в разрезе пользователя. Значение ключа “code” может быть использовано для получения списка всех необходимых полей и их параметров, для выбранного сервиса.

**Response: Success - 200 OK**

```json
[
      {
        "name": "Bank account MD topup",
        "code": "bank_account_md_topup",  
        "country": "MDA",
        "currency_code": "MDL",
        "description": "A service to topup bank account md",
        "type": "SERVICE_BANK"
      },
      {
        "name": "Mastercard transfer to card",
        "code": "mastercard_a2c_md",
        "country": "MDA",
        "currency_code": "MDL",
        "description": "Mastercard transfer to Moldovan card",
        "type": "SERVICE_BANK"
      },
      {
        "name": "Paynet Wallet ",
        "code": "wallet_paynet",
        "country": "MDA",
        "currency_code": "MDL",
        "description": "the best money project, https://paynet.md",
        "type": "SERVICE_WALLET"
      }
   ]
```