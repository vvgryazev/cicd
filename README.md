# Домашнее задание к занятию "Индексы" - `Gryazev Vadim`


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

Задание можно выполнить как в любом IDE, так и в командной строке.
---

### Задание 1

Напишите запрос к учебной базе данных, который вернёт процентное отношение общего размера всех индексов к общему размеру всех таблиц.

#### ОТВЕТ:
SELECT table_schema, sum(index_length / data_length) * 100 "Size in %"
FROM information_schema.TABLES
GROUP BY table_schema
HAVING table_schema = "sakila";

---
### Задание 2

Выполните explain analyze следующего запроса:

select distinct concat(c.last_name, ' ', c.first_name), sum(p.amount) over (partition by c.customer_id, f.title)
from payment p, rental r, customer c, inventory i, film f
where date(p.payment_date) = '2005-07-30' and p.payment_date = r.rental_date and r.customer_id = c.customer_id and i.inventory_id = r.inventory_id


перечислите узкие места;
оптимизируйте запрос: внесите корректировки по использованию операторов, при необходимости добавьте индексы.

#### ОТВЕТ:
-> Limit: 200 row(s)  (actual time=7.38..7.41 rows=200 loops=1)
    -> Sort with duplicate removal: `concat(c.last_name, ' ', c.first_name)`, `sum(p.amount)`  (actual time=7.38..7.39 rows=200 loops=1)
        -> Table scan on <temporary>  (actual time=7.04..7.11 rows=391 loops=1)
            -> Aggregate using temporary table  (actual time=7.04..7.04 rows=391 loops=1)
                -> Nested loop inner join  (cost=507 rows=634) (actual time=0.0934..6.23 rows=634 loops=1)
                    -> Index range scan on p using pay_date over ('2005-07-30 00:00:00' <= payment_date < '2005-07-31 00:00:00'), with index condition: ((p.payment_date >= TIMESTAMP'2005-07-30 00:00:00') and (p.payment_date < <cache>(('2005-07-30' + interval 1 day))))  (cost=286 rows=634) (actual time=0.072..4.84 rows=634 loops=1)
                    -> Single-row index lookup on c using PRIMARY (customer_id=p.customer_id)  (cost=0.25 rows=1) (actual time=0.00191..0.00195 rows=1 loops=634)
---

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
