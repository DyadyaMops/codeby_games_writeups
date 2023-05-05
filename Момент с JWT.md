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


