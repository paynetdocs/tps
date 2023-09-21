# 2. Авторизация и аутентификация
Каждый запрос в системе является уникальным, относительно идентификатора (TPS_API_REQUEST_ID) со стороны партнера в разрезе ключа аутентификации. Повторный запрос с повторяющимся значением будет отвергнут сервером. Для аутентификации запроса необходимо в заголовок каждого запроса подать параметры:   
**TPS_API_KEY** -  Ключ аутентификации  (paynet TPS api key)  
**TPS_API_REQUEST_ID** -  идентификатор запроса (уникальное целочисленное значение )  
**TPS_API_SIGN**   - подпись аутентификации,  каждого запроса ( Your signature authenticating this request. )  

Подпись аутентификации,  вычисляется с помощью алгоритма HMAC-SHA512  (результат - 128 символов) используя шаблон:

Шаблон:
   = HMACSHA512((**TPS_API_KEY + '-TPS-'+ TPS_API_REQUEST_ID**), **secret_password**) 

**Пример расчета подписи аутентификации  на примере данных:** 
TPS_API_KEY:    915281AD-22CA-ED11-8B8E-00155D325A04
TPS_API_REQUEST_ID:   10101,    
TPS_API_PASSWORD:  15A9C2D0-D2DC-4FA8-95FE-2253DE1BBE2D  

</br>

<span style="color:red">Внимание!!! Параметр</span>   TPS_API_REQUEST_ID   <span style="color:red">=  00212   будет конвертирован в 212</span>

</br>

**Пример:**
TPS_API_KEY + '-TPS-'+ TPS_API_REQUEST_ID = “A9CC0276-3766-4827-AB23-5F0EF6017C7C+TPS+10101”

TPS_API_SIGN = HMACSHA512(“A9CC0276-3766-4827-AB23-5F0EF6017C7C+TPS+10101”)  и пароль.   
Результат подсчёта значения подписи:  
```
bced3aec71136dbe9d1122d6636de78751c640f29b64d37528c0cf48ea59845067c6ac3ff29ec64ce6808c8e76f37eade6b57f91d36b13458af00d6fdbc29fa4
```

</br>

## Ответы сервиса при ошибках:

Несовпадение подписи аутентификации, http response code: 400 (Bad Request)
```json
{
    "msg": "Please check access to this service !, ",
    "code": 3003
}
```
</br>

В запросе не подан один из параметров.  http response code: 400 (Bad Request)
```json
{
    "msg": "Please check necessary headers parameters TPS_API_KEY, TPS_API_REQUEST_ID, TPS_API_SIGN",
    "code": 14
}
```
</br>


## Пример расчёта подписи на C#:
```csharp
public static class SecurityHelper
{  
    public static string GetHMACSHA256(string signatureString, string secretKey)
		{	
            UTF8Encoding encoding = new UTF8Encoding();
			byte[] keyByte = encoding.GetBytes(secretKey);
			var hmac = new HMACSHA256(keyByte);
			byte[] messageBytes = encoding.GetBytes(signatureString);
			byte[] hashmessage = hmac.ComputeHash(messageBytes);
			return ByteArrayToHexString(hashmessage);
		}
		
		public static string GetHMACSHA512(string signatureString, string secretKey)
		{
			UTF8Encoding encoding = new UTF8Encoding();
			byte[] keyByte = encoding.GetBytes(secretKey);
			var hmac = new HMACSHA512(keyByte);
			byte[] messageBytes = encoding.GetBytes(signatureString);
			byte[] hashmessage = hmac.ComputeHash(messageBytes);
			return ByteArrayToHexString(hashmessage);
		}

		private static string ByteArrayToHexString(byte[] Bytes)
		{
			StringBuilder Result = new StringBuilder();
			string HexAlphabet = "0123456789ABCDEF";
			foreach (byte B in Bytes)
			{
				Result.Append(HexAlphabet[(int)(B >> 4)]);
				Result.Append(HexAlphabet[(int)(B & 0xF)]);
			}
			return Result.ToString();
		} 	
}
```
