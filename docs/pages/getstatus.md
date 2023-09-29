# 7. Получение статуса операции перевода

**GetStatus**  

| **HTTPS Method** | POST                                                         |
| ---------------- | ------------------------------------------------------------ |
| **Endpoint**     | <span style="color:red">{{Base URL}}</span>//api/Transfers/{transfer_key}<br /><span style="color:red">{{Base URL}}</span>//api/Transfers?partnerExternalId={external_id} |
| **Headers**      | TPS_API_KEY - Ключ аутентификации,<br />TPS_API_KEY - Ключ аутентификации,<br />TPS_API_SIGN - подпись аутентификации |

**Описание**  
Механизм позволяет партнеру производить мониторинг переводов через запросы GetStatus, для получения статуса перевода, используя уникальные идентификаторы (transfer_key).

**Response: Success - <span style="color:green">200 OK</span>**

```json
{
    "reg_date": "2023-06-28 08:52:36",
    "confirm_date": "2023-06-28 08:53:25",
    "amount": 10000,
    "currency_code": "MDL",
    "name": "Mastercard transfer to card",
    "code": "mastercard_a2c_md",
    "clearing_amount": 10415,
    "clearing_currency": "MDL",
    "status": "confirm",
    "transfer_key": "df3311a0-4517-ee11-8b90-00155d325a01",
    "external_id": 1687931555,
        "parameters": 
            {
                "description": "Pentru servicii",
                "receiver_pan": "510188******7449",
                "receiver_first_name": "TestFirst",
                "receiver_last_name": "TestLast",
                "receiver_country": "MDA",
                "sender_first_name": "Tolgahan",
                "sender_last_name": "COLPN",
                "sender_address": "Chisinau str Bogdan-Voievod 22 ap 27",
                "sender_country": "MDA"
            }
}
```
