University: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FTMI](https://ftmi.itmo.ru)  
Course: [Cloud platforms as the basis of technology entrepreneurship](https://https://itmo-ict-faculty.github.io/cloud-platforms-as-the-basis-of-technology-entrepreneurship/)  
Year: 2024/2025  
Group: U4225  
Author: Makedonskii Daniil Dmitrievich  
Lab: Lab2
Date of create: 30.10.2024  
Date of finished: 01.11.2024  

В данной лабораторной работе необходимо создать Cloud Run из стандартного инструментария

1. Создаем первый Cloud Run с портом 8080 на сервере north europe (Finland)
Деплой контейнера:
![pic1./1.png](/lab2/1.png) 
2. После создания смотрим на логи, где содержится информация о создании, имени, порте, сервере. Контейнер создан в Google Cloud Console на сервере europe-north1 c портом 8080:
![pic2./2.png](/lab2/2.png)
3. Нам доступны метрики:
Request Count, Request latencies, Container instance count, Billable container instance time, Container CPU utilisation, Container memory utilisitaion, Sent bytes, Received bytes, Max concurrent request, Container startrup latancy. В некоторых метриках есть активность, это связано с деплоем контейнера и просмотром информации о нем по URL Cloud Run:
![pic3./3.png](/lab2/3.png)
4. Создаем альтернативный контейнер с портом 8090 (порт для веб-сервисов). Контейнер успешно создан:
![pic4./4.png](/lab2/4.png)
5. Обновленные логи с инфорамацией об успешном деплое на том же сервере:
![pic5./5.png](/lab2/5.png)
6. Обновленные метрики. Активность изменилась, например, в метрике Max. concurrent request, Sent bytes (количество отправленных байтов - снизилось до нуля), Container instance count - стало 0
![pic6./6.png](/lab2/6.png)
7. Распределяем трафик между версиями в соотношении 90% и 10%  смотрим на лог, который отражает изменение:
![pic7./7.png](/lab2/7.png)
8. Меняем распределение на 50%/50%. В логах видно, что мы обращаемся к странице с деплоем контейнера (GET 200)
![pic8./8.png](/lab2/8.png)
9. В результате многократного переключения трафика он распределяется неравномерно, отслеживаем его по метрике Request Count. Она показывает, что большинство запросов приходится на первую версию контейнера, на которую в некоторых случах приходилось 90% трафика
![pic9./9.png](/lab2/9.png)

Таким образом, обновление контейнеров позволяет перераспределять трафик, чтобы контролировать и тестировать разные версии
