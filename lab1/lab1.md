University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FTMI](https://ftmi.itmo.ru)  
Course: [Cloud platforms as the basis of technology entrepreneurship](https://https://itmo-ict-faculty.github.io/cloud-platforms-as-the-basis-of-technology-entrepreneurship/)  
Year: 2024/2025  
Group: U4225  
Author: Makedonskii Daniil Dmitrievich  
Lab: Lab1  
Date of create: 30.10.2024  
Date of finished: 01.11.2024  

Для данной лабораторной работы необходимо создать сервисный аккаунт 
на платформе Google Cloud. Ниже дан скриншот с созданным аккаунтом в списке 
email - daniilmaks@gmail.com
![pic1./1.png](/lab1/1.png)
После создания профиля переходим к виртуальной машине
Создаем минимальный compute engine (виртуальную машину) 
с Machine type e2-micro в режиме spot
Интерфейс создания:
![pic2./2.png](/lab1/2.png)
Созданная VM
![pic3./3.png](/lab1/3.png)

Далее с помощью gsutils открываем Lab1-bucket-itmo и убеждаемся, что там 3 файла, которые копируем к себе в директорию и проверяем
командой ls -lah
![pic4./4.png](/lab1/4.png)

Меняем права пользователя с уровня Storage Admin до уровня Compute Viewer, повторяем операцию с копироаванием - отказано в доступе
![pic5./5.png](/lab1/5.png)

##Итоги
В роли Storage Admin можно распоряжаться файлами, бакетами и остальными ресурсами как угодно, при измении роли на Compute Engine права сильно урезаются - можно только просматривать хранилища, без доступа к файлам
