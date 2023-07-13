### Домашнее задание к занятию «Работа с данными (DDL/DML)» - Корольков Денис

Задание можно выполнить как в любом IDE, так и в командной строке.

### Задание 1
1.1. Поднимите чистый инстанс MySQL версии 8.0+. Можно использовать локальный сервер или контейнер Docker.

Ответ:

Подробное описание как я поднимал mysql server описан в документе Google - ссылка в конце работы.

Здесь выкладываю результат:

ставим сам MySQL 8
```
apt install mysql-server
```
Проверяю статус сервера mysql:

```
systemctl status mysql
```
![screen1](https://github.com/KorolkovDenis/)

1.2. Создайте учётную запись sys_temp. 

Захожу в БД MySQL под пользователем root:

```
mysql –u root –p
```
Далее ввожу команду:

```
CREATE USER ‘sys_temp’@’localhost’ IDENTIFIED BY ‘debian’;
```
![screen2](https://github.com/KorolkovDenis/)

1.3. Выполните запрос на получение списка пользователей в базе данных. (скриншот)

Смотрим наших пользователей:
```
SELECT User,Host FROM mysql.user;
```
![screen3](https://github.com/KorolkovDenis/)

1.4. Дайте все права для пользователя sys_temp. 

Даю права доступа для sys_temp – ALL PRIVILEGES. Так как у меня сейчас нет созданных БД, ставлю ‘*’ –  ON * - то есть выбираю все БД и все таблицы - *TO. 

![screen4](https://github.com/KorolkovDenis/)

По правам у меня получился так называемый SUPERUSER.

1.5. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

Теперь посмотрим привилегии нашего пользователя:
```
SHOW GRANTS FOR ‘sys_temp’@’localhost’;
```

![screen5](https://github.com/KorolkovDenis/)

1.6. Переподключитесь к базе данных от имени sys_temp.

Для смены типа аутентификации с sha2 используйте запрос: 
```sql
ALTER USER 'sys_test'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
```
mysql – u sys_temp -p
```
![screen6](https://github.com/KorolkovDenis/)

1.6. По ссылке https://downloads.mysql.com/docs/sakila-db.zip скачайте дамп базы данных.

1.7. Восстановите дамп в базу данных.

БД восстанавливал через терминал:
Сперва создал БД (sakila):
```
mysql –u root -p
CREATE DATABASE sakila DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci 
```
![screen7](https://github.com/KorolkovDenis/)

Затем закинул в БД содержание:
```
mysql –u root –p sakila <home/korolkov/Загрузки/sakila-db/sakila-schema.sql
mysql –u root –p sakila <home/korolkov/Загрузки/sakila-db/sakila-data.sql
```

1.8. При работе в IDE сформируйте ER-диаграмму получившейся базы данных. При работе в командной строке используйте команду для получения всех таблиц базы данных. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*

Открываю Dbeaver – смотрим диаграмму БД

![screen8](https://github.com/KorolkovDenis/)

теперь через консоль:

![screen9](https://github.com/KorolkovDenis/)

### Задание 2
Составьте таблицу, используя любой текстовый редактор или Excel, в которой должно быть два столбца: в первом должны быть названия таблиц восстановленной базы, во втором названия первичных ключей этих таблиц. Пример: (скриншот/текст)
```
Название таблицы | Название первичного ключа
customer         | customer_id
```
Ответ:

```
Название таблицы	Название первичного ключа
actor	            actor_id
address	            address_id
category	        category_id
city	            city_id
country	            country_id
customer	        customer_id
film	            film_id
film_actor	        actor_id, film_id
film_category	    category_id, film_id
film_text	        film_id
inventory	        inventory_id
language	        language_id
payment	            payment_id
rental	            rental_id
staff	            staff_id
store	            store_id
```

## Дополнительные задания (со звёздочкой*)
Эти задания дополнительные, то есть не обязательные к выполнению, и никак не повлияют на получение вами зачёта по этому домашнему заданию. Вы можете их выполнить, если хотите глубже шире разобраться в материале.

### Задание 3*
3.1. Уберите у пользователя sys_temp права на внесение, изменение и удаление данных из базы sakila.

```
REVOKE DELETE ON *.* FROM ‘sys_temp’@’localhost’;
REVOKE  ALTER ON *.* FROM ‘sys_temp’@’localhost’;
REVOKE CREATE ON *.* FROM ‘sys_temp’@’localhost’;
FLUSH PRIVILEGES;
```

### Вопрос: Почему то не получилось убрать права конкретно для БД sakila. Пришлось убирать права на все БД для учетки: sys_temp.

![screen10](https://github.com/KorolkovDenis/)

3.2. Выполните запрос на получение списка прав для пользователя sys_temp. (скриншот)

*Результатом работы должны быть скриншоты обозначенных заданий, а также простыня со всеми запросами.*
```
SHOW GRANTS FOR ‘sys_temp’@’localhost’;
```

![screen11](https://github.com/KorolkovDenis/)


[Cсылка на google docs по «Работа с данными (DDL/DML)» - полное описание](https://docs.google.com/)