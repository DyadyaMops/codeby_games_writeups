# Разминка с JWT

При переходе по ссылке мы видим некий скрипт на питоне.  

![image](https://user-images.githubusercontent.com/115101419/236478581-630585fe-5e56-4863-a5e8-effe61085651.png)

Мы видим в нём две функции: /gen-jwt/{name} и /check-jwt

При переходе по директории /gen-jwt у нас будет генерироваться JWT токен для какого-то {name}.
Для примера возьмем {name} admin и перейдем по этой ссылке

![image](https://user-images.githubusercontent.com/115101419/236479367-0246d4cb-0b12-4171-ad05-ab6ae43135b2.png)
 
 Токен ожидаемо сгенерировался
 Первое что приходит в голову это воспользоваться jwt decoder'ом чтобы посмотреть какие параметры в токене присутствуют
 
 Воспользуемся [jwt.io](https://jwt.io/)
 
 ![image](https://user-images.githubusercontent.com/115101419/236480328-21e9ed67-b517-4834-8eec-8796c8549bd3.png)

Видим, что у нас есть стандартный заголовок, а также поля name, куда подставляется вводимое имя и поле isAdmin, равное false
Попробуем поменять isAdmin на true и проверить измененный токен
 
 ![image](https://user-images.githubusercontent.com/115101419/236481389-a8d1e07c-f5c5-4a76-8965-62854f00c930.png)

Ошибка о том, что проверка сигнатуры провалена!
Казалось бы тупик, ведь мы не знаем какая подпись у токена
Но вспоминаем хинт!
![image](https://user-images.githubusercontent.com/115101419/236482069-57e713b5-9d84-4c5f-b599-556693eff57e.png)

Попробуем ввести CODEBY{ как подпись

![image](https://user-images.githubusercontent.com/115101419/236482266-265947c0-ba7e-4c63-b866-c7a904ed54e6.png)
 
 Проверяем
 
 ![image](https://user-images.githubusercontent.com/115101419/236482325-abf65050-b15b-4dca-8ffe-5d7ef1db16c7.png)

Таск решен!

**CODEBY{JWT_WARMUP_FLAG}**

