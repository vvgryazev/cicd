
#  Дипломная работа по профессии «Системный администратор»

Содержание
==========
* [Задача](#Задача)
* [Инфраструктура](#Инфраструктура)
    * [Сайт](#Сайт)
    * [Мониторинг](#Мониторинг)
    * [Логи](#Логи)
    * [Сеть](#Сеть)
    * [Резервное копирование](#Резервное-копирование)
    * [Дополнительно](#Дополнительно)
* [Выполнение работы](#Выполнение-работы)
* [Критерии сдачи](#Критерии-сдачи)
* [Как правильно задавать вопросы дипломному руководителю](#Как-правильно-задавать-вопросы-дипломному-руководителю) 

---------

## Задача
Ключевая задача — разработать отказоустойчивую инфраструктуру для сайта, включающую мониторинг, сбор логов и резервное копирование основных данных. Инфраструктура должна размещаться в [Yandex Cloud](https://cloud.yandex.com/) и отвечать минимальным стандартам безопасности.
 

### Сайт
Создайте две ВМ в разных зонах, установите на них сервер nginx, если его там нет. ОС и содержимое ВМ должно быть идентичным, это будут наши веб-сервера.

![jenkins](/img/200.PNG)

Создайте [Target Group](https://cloud.yandex.com/docs/application-load-balancer/concepts/target-group), включите в неё две созданных ВМ.

![jenkins](/img/201.PNG)

Создайте [Backend Group](https://cloud.yandex.com/docs/application-load-balancer/concepts/backend-group), настройте backends на target group, ранее созданную. Настройте healthcheck на корень (/) и порт 80, протокол HTTP.

![jenkins](/img/202.PNG)

Создайте [HTTP router](https://cloud.yandex.com/docs/application-load-balancer/concepts/http-router). Путь укажите — /, backend group — созданную ранее.

![jenkins](/img/203.PNG)

Создайте [Application load balancer](https://cloud.yandex.com/en/docs/application-load-balancer/) для распределения трафика на веб-сервера, созданные ранее. Укажите HTTP router, созданный ранее, задайте listener тип auto, порт 80.


![jenkins](/img/205.PNG)

Протестируйте сайт
`curl -v <публичный IP балансера>:80` 

![jenkins](/img/2041.png)

### Мониторинг
Создайте ВМ, разверните на ней Zabbix. На каждую ВМ установите Zabbix Agent, настройте агенты на отправление метрик в Zabbix. 

Настройте дешборды с отображением метрик, минимальный набор — по принципу USE (Utilization, Saturation, Errors) для CPU, RAM, диски, сеть, http запросов к веб-серверам. Добавьте необходимые tresholds на соответствующие графики.
![jenkins](/img/20611.png)


### Логи
Cоздайте ВМ, разверните на ней Elasticsearch. Установите filebeat в ВМ к веб-серверам, настройте на отправку access.log, error.log nginx в Elasticsearch.

Создайте ВМ, разверните на ней Kibana, сконфигурируйте соединение с Elasticsearch.

![jenkins](/img/210.PNG)

Elasticsearch на ВМ развернут с помощью ansibe ansible/elasticsearch.yaml

Проверка состояния кластера.

![jenkins](/img/211.PNG)

Filebeat на ВМ развернут с помощью ansibe ansible/filebeat.yaml

Проверка доступности elasticsearch.


![jenkins](/img/212.PNG)
![jenkins](/img/213.PNG)

Создайте ВМ, разверните на ней Kibana, сконфигурируйте соединение с Elasticsearch.
![jenkins](/img/214.PNG)

Kibana на виртуальной машине развернута с использованием ansibe ansible/kibana.yaml

Веб-консоль kibana доступна из сети интернет по адресу http://51.250.28.206:5601

Данные для авторизации: Логин-elastic Пароль-aA48HS5t8dU=PyoPlLch

Логи отправляются в elasticsearch.

### Сеть
Разверните один VPC. Сервера web, Elasticsearch поместите в приватные подсети. Сервера Zabbix, Kibana, application load balancer определите в публичную подсеть. Настройте Security Groups соответствующих сервисов на входящий трафик только к нужным портам.

![jenkins](/img/230.PNG)
![jenkins](/img/231.PNG)

### Резервное копирование
Создайте snapshot дисков всех ВМ. Ограничьте время жизни snaphot в неделю. Сами snaphot настройте на ежедневное копирование.

![jenkins](/img/300.PNG)




