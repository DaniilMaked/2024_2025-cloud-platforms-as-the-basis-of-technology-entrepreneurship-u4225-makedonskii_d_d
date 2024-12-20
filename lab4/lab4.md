wUniversity: [ITMO University](https://itmo.ru/ru/)  
Faculty: [FTMI](https://ftmi.itmo.ru)  
Course: [Cloud platforms as the basis of technology entrepreneurship](https://https://itmo-ict-faculty.github.io/cloud-platforms-as-the-basis-of-technology-entrepreneurship/)  
Year: 2024/2025  
Group: U4225  
Author: Makedonskii Daniil Dmitrievich  
Lab: Lab4
Date of create: 02.10.2024  
Date of finished: 05.11.2024  
В данной лабораторной работе необходимо описать идею AI-приложения, приложить схему работы, примерную стоимость и обосновать выбор

Приложение - система мониторинга лесных пожаров на основе AI. Приложением пользуются профильные службы (пожарная служба, лесоохрана, служба ООПТ, национальных парков и т.д.)
#####  Схема инфраструктуры AI-приложения ##### 
![pic1./firebase.png](/lab4/firebase.png)
##### Данные ##### 
Данные поступают из нескольких источников - это сообщения пользователей, спутниковые снимки, метеостанции, специальные датчики
##### Cloud Load Balancing ##### 
Встроенный сервис Google Cloud, который распределяет нагрузка между виртуальными машинами. Благодаря ему всегда можно перенаправить трафик на резервную машину и повысить надежность системы
#####  Compute Engine ##### 
Серверы, на которые поступают данные. Выбраны средней мощности, для соблюдения баланса производительности и стоимости
#####  Openstreetmap API ##### 
Бесплатный API для определения геоданных
#####  Cloud SQL ##### 
Используется для хранения упорядоченных данных и выполнения запросов
#####  PostGIS ##### 
Внешняя SQL-совместимая база данных, которая поддерживает геоданные и обменивается информацией с CloudSQL. Бесплатная. Также является резервной для данных из Cloud SQL
#####  Cloud Storage ##### 
База данных для хранения неструктированных данных (растровые снимки и др.)
#####  Dataflow ##### 
Инструмент для обработки данных и подготовки к обучению
#####  Mapflow AI ##### 
Специализированный AI для работы с геоданными - принимает, обучается, распознает по необходимому сценарию (в данном случае определяет наличие лесных пожаров)
#####  Leaflet ##### 
Библиотека JavaScript, которая позволяет визуализировать геоданные и встраивать в интерактивные веб-карты. Бесплатно
#####  Конечный UI - карта ##### 
Пользователи (например, служба национальных парков), видят информацию об очаге пожара на веб-карте, которая работает через leaflet и принимают решение
##### Data Loss Prevention API ##### 
Инструмент, который предотвращает утечки данных и следит за конфиденциальностью, обезличивая данные

##### Выбор ресурсов и расчет ##### 
При разработке MVP важно соблюдать баланс между ценой и производительностью. Большинство компонентов Google Cloud средней или малой мощности/объема, чтобы протестировать работу сервиса на небольшом объеме геоданных (например, несколько регионов небольшой площади - Северный Кавказ). 2 сервера средней мощности обеспечивают достаточную производительность и надежность, 2 хранилища для разных типов данных позволяют хранить и обрабтывать всю поступающую информацию. 

Все выбранные серверы Google Cloud находятся в Европе, в Хельсинки, так как это экономит ресурсы, снижает воздействие на окружающую среду (при выборе данной локации Google говорит о снижении выбросов CO2), снижает стоимость и в целом реализуемый сервис для небольших регионов более актуален в Европе и Европейской части России, где регионы (АТД 1-го уровня) не так велики.

Все сторонние используемые сервисы бесплатны и являются популярными open-source-решениями - Openstreetmap, PostGIS, Leaflet, Mapflow AI (есть платные версии для более высокой производительности - для MVP достаточно бесплатной версии или версии за 50$/месяц). Таким образом, цена складывается из компонентов Google Cloud. Примерный расчет:
![pic1./calc.png](/lab4/calc.png)
https://cloud.google.com/products/calculator?hl=ru&dl=CjhDaVE1TkdWbE9HTTNNeTA0TW1JekxUUTFNak10T1RCbE9DMHhOelZtTkdRME5HWmxZMllRQVE9PRAsGiQwOTgxOTE2RS1ERjE3LTRCMkYtQUUwNy0zRkVGRkI1QUY3OTI

