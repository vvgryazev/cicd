# Домашнее задание к занятию "Базы данных" - `Gryazev Vadim`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректнго добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1.

Легенда
Заказчик передал вам файл в формате Excel, в котором сформирован отчёт.

На основе этого отчёта нужно выполнить следующие задания.

Опишите не менее семи таблиц, из которых состоит база данных:

какие данные хранятся в этих таблицах;
какой тип данных у столбцов в этих таблицах, если данные хранятся в PostgreSQL.
Приведите решение к следующему виду:

Сотрудники (

идентификатор, первичный ключ, serial,
фамилия varchar(50),
...
идентификатор структурного подразделения, внешний ключ, integer).


Ответ: 

Сотрудники:

ФИО сотрудника (Фамилия, Имя, Отчество) - varchar(50)
Оклад (Оклад) - numeric(8, 2)
Должность (Должность) - varchar(50)
Тип подразделения (Тип_подразделения) - varchar(50)
Структурное подразделение (Структурное_подразделение) - varchar(100)
Дата найма (Дата_найма) - date
Адрес филиала (Адрес_филиала) - varchar(200)
Проект на который назначен (Проект) - varchar(100)
Структурные подразделения (Departments):
Идентификатор структурного подразделения (идентификатор, первичный ключ, serial)
Название структурного подразделения (Название) - varchar(100)

Проекты:

Идентификатор проекта (идентификатор, первичный ключ, serial)
Название проекта (Название) - varchar(100)

Филиалы:

Идентификатор филиала (идентификатор, первичный ключ, serial)
Адрес филиала (Адрес) - varchar(200)

Должности:

Идентификатор должности (идентификатор, первичный ключ, serial)
Название должности (Название) - varchar(50)

Типы подразделений:

Идентификатор типа подразделения (идентификатор, первичный ключ, serial)
Название типа подразделения (Название) - varchar(50)

Оклад:

Идентификатор оклала (идентификатор, первичный ключ, serial)
Оклад (Оклад) - numeric(8, 2)






## Дополнительные задания (со звездочкой*)

Эти задания дополнительные (не обязательные к выполнению) и никак не повлияют на получение вами зачета по этому домашнему заданию. Вы можете их выполнить, если хотите глубже и/или шире разобраться в материале.

### Задание 

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
