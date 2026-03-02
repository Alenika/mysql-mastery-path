### Упражнения: Внутреннее соединение INNER JOIN
**Источник** [sql-academy.org](https://sql-academy.org/ru/guide/inner-join)

#### Задача 1. INNER JOIN
**Условиe** Объедините таблицы `Class` и `Student_in_class` с помощью внутреннего соединения по полям `Class.id` и `Student_in_class.class`. Выведите название класса (поле `Class.name`) и идентификатор ученика (поле `Student_in_class.student`).

```sql
SELECT 
    Class.name, 
    Student_in_class.student
FROM Class
INNER JOIN Student_in_class
    ON Class.id = Student_in_class.class;
```

#### Задача 2.  Многотабличный INNER JOIN
**Условиe** Дополните запрос из предыдущего задания, добавив ещё одно внутреннее соединение с таблицей `Student`. Объедините по полям `Student_in_class.student` и `Student.id` и вместо идентификатора ученика выведите его имя (поле `first_name`).

```sql
SELECT Class.name, Student.first_name
FROM Class
INNER JOIN Student_in_class
    ON Class.id = Student_in_class.class
INNER JOIN Student
    ON Student_in_class.student = Student.id;
```

#### Задача 3. Многотабличный INNER JOIN с фильтрацией строк
**Условиe** Выведите названия продуктов, которые покупал член семьи со статусом "son". Для получения выборки вам нужно объединить таблицу `Payments` с таблицей `FamilyMembers` по полям `family_member` и `member_id`, а также с таблицей `Goods` по полям `good` и `good_id`.

```sql
SELECT Goods.good_name
FROM Payments
INNER JOIN FamilyMembers
    ON Payments.family_member = FamilyMembers.member_id
INNER JOIN Goods
    ON Payments.good = Goods.good_id
WHERE FamilyMembers.status = 'son';
```

#### Задача 4. INNER JOIN с группировкой
**Условиe** Выведите идентификатор (поле `room_id`) и среднюю оценку комнаты (поле `rating`, для вывода используйте псевдоним `avg_score`), составленную на основании отзывов из таблицы `Reviews`.
Данная таблица связана с `Reservations` (таблица, где вы можете взять идентификатор комнаты) по полям `reservation_id` и `Reservations.id`.

```sql
SELECT Reservations.room_id,
       AVG(Reviews.rating) AS avg_score
FROM Reviews
INNER JOIN Reservations
    ON Reviews.reservation_id = Reservations.id
GROUP BY Reservations.room_id;
```

### Упражнения: Внешнее соединение OUTER JOIN
**Источник** [sql-academy.org](https://sql-academy.org/ru/guide/outer-join)

#### Задача 1. Внешнее левое соединение
**Условиe** Выведите имя `first_name` и фамилию `last_name` каждого учителя из таблицы `Teacher`, а также количество занятий, в которых он был назначен преподавателем. Если преподаватель не был назначен ни на одно занятие, то выведите 0.
Для вывода количества занятий используйте псевдоним `amount_classes`.

```sql
SELECT
    Teacher.first_name,
    Teacher.last_name,
    COUNT(Schedule.id) AS amount_classes
FROM Teacher
LEFT JOIN Schedule
    ON Teacher.id = Schedule.teacher
GROUP BY
    Teacher.id,
    Teacher.first_name,
    Teacher.last_name;
```

### Упражнения: Ограничение выборки, оператор LIMIT
**Источник** [sql-academy.org](https://sql-academy.org/ru/guide/limit)

#### Задача 1. Ограничение записей с начала таблицы
**Условиe** Отсортируйте список компаний (таблица `Company`) по их названию в алфавитном порядке и выведите первые две записи.

```sql
SELECT * FROM company
ORDER BY Name
LIMIT 2;
```

