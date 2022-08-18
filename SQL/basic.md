<a name="menu"></a>
## Меню

* [Главная страница](https://github.com/CodeWormD/cheat_sheets)

* [Создание таблицы](#create)
* [Базовые запросы](#base)
* [JOIN](#join)
    * [INNER JOIN](#innerjoin)
    * [LEFT JOIN](#leftjoin)
    * [RIGHT JOIN](#rightjoin)
    * [FULL JOIN](#fulljoin)
    * [CROSS JOIN](#crossjoin)
* Изменение таблицы - [ALTER TABLE](#update)
    * [Переименование таблицы](#rename)
    * [Добавление колонки](#add_col)
    * [Переименование колонки](#renam_col)
    * [Удаление колонки](#del_col)
    * [Удаление таблиц](#del_tab)
    * [Ссылочная целостность](#linksstable)




<a name="create"></a>
## Пример создание таблицы

``` SQL
CREATE TABLE IF NOT EXISTS toppings(
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE IF NOT EXISTS ice_cream(
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE IF NOT EXISTS ice_cream_toppings(
    id INTEGER PRIMARY KEY,
    ice_cream_id INTEGER,
    topping_id INTEGER NOT NULL,
    PRIMARY KEY (ice_cream_id, toppings_id),
    FOREIGN KEY(ice_cream_id) REFERENCES ice_cream(id),
    FOREIGN KEY(topping_id) REFERENCES toppings(id)
); 
```
##### ([Вернуться к оглавлению](#menu))

<a name="base"></a>
## Базовые запросы

``` SQL
SELECT ('столбцы (* - для выбора всех столбцов); обязательно')
(могут применяться агрегатные функции COUNT, MIN, MAX, AVG и SUM; необязательно)
(и ключевое слово DISTINCT; необязательно)
```
``` SQL
FROM ('таблица; обязательно')
```
``` SQL
WHERE ('условие/фильтрация; необязательно')
```
``` SQL
GROUP BY ('столбец, по которому нужно сгруппировать данные; необязательно')
```
``` SQL
HAVING ('условие/фильтрация на уровне сгруппированных данных; необязательно')
используется в сочетании с оператором GROUP BY, чтобы ограничить группы возвращаемых строк только теми, чьё условие TRUE.
```
```SQL
ORDER BY ('столбец, по которому нужно ранжировать вывод; необязательно')
```
``` SQL
OFFSET ('начиная с какой записи показывать; необязательно')
```
``` SQL
LIMIT ('сколько записей показывать; необязательно')
```
##### ([Вернуться к оглавлению](#menu))


<a name="join"></a>
## Объединение таблиц - JOIN

<a name="innerjoin"></a>
* INNER JOIN 

Оператор INNER JOIN включает в результирующую таблицу только те записи, в которых выполняется условие, заданное в ON

``` SQL
SELECT movies.name,
       slogans.name,
       types.name
FROM movies
JOIN slogans ON movies.slogan_id = slogans.id
JOIN types ON movies.type_id = types.id;
```
##### ([Вернуться к оглавлению](#menu))

<a name="leftjoin"></a>
* LEFT OUTER JOIN

При обработке запроса LEFT JOIN объединяемые таблицы условно называют «левая» и «правая». «Левая» — та, которая вызвана в блоке FROM, «правая» — та, что указана после ключевого слова JOIN. «Правых» таблиц может быть и несколько.

``` SQL
SELECT movies.name,
       slogans.name
FROM movies
LEFT JOIN slogans ON movies.slogan_id = slogans.id; 
```
##### ([Вернуться к оглавлению](#menu))

<a name="rightjoin"></a>
* RIGHT OUTER JOIN

RIGHT JOIN – это такое же объединение, как и LEFT JOIN, но выводятся все записи из правой таблицы, а к ним добавляются только те данные из левой таблицы, в которых есть ключ объединения.

``` SQL
SELECT movies.name,
       types.name
FROM movies
RIGHT JOIN types ON movies.type_id = types.id; 
```
##### ([Вернуться к оглавлению](#menu))

<a name="fulljoin"></a>
* FULL OUTER JOIN

При запросе FULL (OUTER) JOIN выводятся все записи из объединяемых таблиц. Те записи, у которых запрошенные значения совпадают — выводятся парами, у остальных недостающее значение заменяется на NULL (Python выведет None).

Другими словами, FULL JOIN == LEFT JOIN + RIGHT JOIN.

``` SQL
SELECT movies.name,
       slogans.name
FROM movies
FULL JOIN slogans ON movies.slogan_id = slogans.id;  
```
##### ([Вернуться к оглавлению](#menu))

<a name="crossjoin"></a>
* CROSS JOIN

Объединение таблиц через CROSS JOIN возвращает декартово произведение таблиц — каждая запись левой таблицы объединится с каждой записью правой. Параметр ON при запросах CROSS JOIN не применяется.

``` SQL
SELECT movies.name,
       slogans.name
FROM movies
CROSS JOIN slogans; 
```
##### ([Вернуться к оглавлению](#menu))


<a name="update"></a>
## Изменение таблицы - ALTER TABLE

<a name="rename"></a>
### Переименование таблицы
``` SQL
ALTER TABLE <имя таблицы> RENAME TO <новое имя таблицы>; 
```

<a name="add_col"></a>
### Добавление колонки

``` SQL
ALTER TABLE <название таблицы> 
ADD COLUMN <имя колонки> <тип колонки>;
```

<a name="rename_col"></a>
### Переименование колонки
``` SQL
ALTER TABLE <название таблицы>
RENAME COLUMN <старое имя колонки> TO <новое имя колонки>; 
```

<a name="del_col"></a>
### Удаление колонки

``` SQL
ALTER TABLE <название таблицы>
DROP COLUMN <имя колонки>; 
```

<a name="del_tab"></a>
### Удаление таблицы

``` SQL
DROP TABLE <имя таблицы>; 
```

<a name="linksstable"></a>
### Ссылочная целостность


* Аномалия удаления (deletion anomaly): если из таблицы удалена строка, на которую ссылается внешний ключ.

* Аномалия вставки (insertion anomaly): если добавлена запись с внешним ключом, но этот внешний ключ не соответствует ни одному первичному ключу из связанной таблицы.

* Аномалии обновления (update anomaly): при изменении данных в одной строке они могут прийти в противоречие с данными из другой строки: например, изменён PK, на который ссылкется FK из другой таблицы.

##### ([Вернуться к оглавлению](#menu))
