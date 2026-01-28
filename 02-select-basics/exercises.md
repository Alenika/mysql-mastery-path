### 📋 Упражнения: Базовый синтаксис SELECT 
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/basic-syntax-sql-query)

#### Задача 1. Вывод строки  
**Условие:** С помощью оператора SELECT выведите текст "Hello world"  
```sql
SELECT 'Hello world';
```

#### Задача 2. SELECT по всем столбцам  
**Условие:** Выведите все столбцы из таблицы Payments.  
```sql
SELECT *
FROM Payments;
```

#### Задача 3. SELECT по нескольким столбцам  
**Условие:** Выведите поля member_id, member_name и status из таблицы FamilyMembers.  
```sql
SELECT member_id, member_name, status
FROM FamilyMembers;
```

#### Задача 4. Вывод с псевдонимами
**Условие:** Выведите поле name из таблицы Passenger. При выводе данного поля используйте псевдоним "passengerName"
```sql
SELECT name AS passengerName
FROM Passenger;
```

--- 

### 📋 Упражнения: Применение функций 
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/using-functions)

#### Задача 1. Вывод строки в нижнем регистре  
**Условие:** Выведите текст "Hello world" в нижнем регистре с помощью соответствующей функции.  
```sql
SELECT LOWER('Hello world') AS lower_string;
```

#### Задача 2. Вывод года из даты  
**Условие:** Выведите полное имя члена семьи и его год рождения, используя функцию YEAR.  
Для вывода года рождения используйте псевдоним year_of_birth.   
```sql
SELECT member_name, YEAR(birthday) AS year_of_birth
FROM FamilyMembers;
```

#### Задача 3. Вычисление длины фамилии  
**Условие:** Выведите полное имя члена семьи и длину его фамилии.    
Для вывода длины фамилии используйте псевдоним lastname_length.    
```sql
SELECT member_name, 
LENGTH(member_name) - INSTR(member_name, ' ') AS lastname_length
FROM FamilyMembers;
```

---

### 📋 Упражнения: Исключение дубликатов, DISTINCT 
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/distinct-operator)

#### Задача 1. Вывод уникальных имён
**Условие:** Выведите только уникальные имена first_name студентов из таблицы Student.  
```sql
SELECT DISTINCT first_name 
FROM Student;
```

#### Задача 2. Вывод уникальных пар колонок
**Условие:** Выведите только уникальные пары значений идентификатор учителя teacher и идентификатор предмета subject из таблицы Schedule. Пара 2, 3 отличается от 3, 2.  
```sql
SELECT DISTINCT 
    teacher, 
    subject 
FROM Schedule;
```

---

### 📋 Упражнения: Условный оператор WHERE 
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/conditional-where-operator)

#### Задача 1. Простая фильтрация по числам
**Условие:** Выведите идентификаторы товаров (поле good) из таблицы Payments, стоимость которых больше 2000 единиц. Стоимость товара хранится в поле unit_price.

```sql
SELECT good
FROM Payments
WHERE unit_price > 2000;
```

#### Задача 2. Простая фильтрация по строкам
**Условие:** Выведите имена (поле member_name) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father".

```sql
SELECT member_name
FROM FamilyMembers
WHERE status = 'father';
```

#### Задача 3. Логическое ИЛИ
**Условие:** Выведите имя (поле member_name) и дату рождения (поле birthday) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father" или "mother".

```sql
SELECT member_name, birthday 
FROM FamilyMembers
WHERE status = 'father' OR status = 'mother';
```

#### Задача 4. Логическое И
**Условие:** Необходимо получить все комнаты, в которых есть как кухня (поле has_kitchen), так и интернет (поле has_internet). Напишите запрос, удовлетворяющий вышеописанному условию, который выводит все поля из таблицы Rooms.
Наличие обозначается 1 или true, а отсутствие 0 или false.

```sql
SELECT * 
FROM Rooms
WHERE has_kitchen = true AND has_internet = true;
```

---

### 📋 Упражнения: Операторы IS NULL, BETWEEN, IN 
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/is-null-between-in-operators)

#### Задача 1. Вывод записей, содержащих NULL
**Условие:** Выведите имена first_name и фамилии last_name студентов из таблицы Student, у кого отсутствует отчество middle_name.

```sql
SELECT first_name, last_name FROM Student
WHERE middle_name IS NULL;
```

#### Задача 2. Поиск значений в указанном промежутке
**Условие:** Выведите резервации комнат (поля room_id, start_date, end_date) из таблицы Reservations, у которых итоговая стоимость аренды (поле total) находится в промежутке от 500 до 1200 включительно.

```sql
SELECT room_id, start_date, end_date FROM Reservations
WHERE total BETWEEN 500 AND 1200;
```

#### Задача 3. Поиск значений, входящий в определенный список
**Условие:** Выведите информацию о студентах из таблицы Student, у которых год рождения соответствует одному из перечисленных: 2000, 2002 и 2004.

```sql
SELECT * FROM Student
WHERE YEAR(birthday) IN (2000, 2002, 2004);
```

---

### 📋 Упражнения: Оператор LIKE
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/operator-like)

#### Задача 1. Поиск по строковому шаблону
**Условие:** Найдите всех членов семьи с фамилией "Quincey" и выведите поле member_name.

```sql
SELECT member_name 
FROM FamilyMembers
WHERE member_name LIKE '%Quincey';
```

---

### 📋 Упражнения: Оператор REGEXP для регулярных выражений
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/operator-regexp)

#### Задача 1. Поиск по подстроке
**Условие:** Найдите все жилые помещения (таблица Rooms), в адресе которых содержится строка «Avenue». В результирующей выборке выведите поля id и address.

```sql
SELECT id, address FROM Rooms
WHERE address REGEXP 'Avenue';
```

#### Задача 2. Поиск по электронной почте
**Условие:** Выведите name, email пользователей, чей адрес электронной почты заканчивается на «@outlook.com» или «@live.com».

```sql
SELECT name, email FROM Users
WHERE email REGEXP '@outlook.com|@live.com';
```

---

### 📋 Упражнения: Сортировка, оператор ORDER BY
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/sorting)

#### Задача 1. Сортировка по убыванию
**Условие:** Для каждого отдельного платежа выведите идентификатор товара и сумму, потраченную на него, в отсортированном по убыванию этой суммы виде. Список платежей находится в таблице Payments.
Для вывода суммы используйте псевдоним sum.

```sql
SELECT good, (unit_price * amount) AS sum 
FROM Payments
ORDER BY sum DESC;
```

#### Задача 2. Сортировка по нескольким столбцам
**Условие:** Выведите все данные членов семьи с фамилией Quincey из таблицы FamilyMembers и отсортируйте их по возрастанию сначала по столбцу status, а затем по member_name.

```sql
SELECT * FROM FamilyMembers
WHERE member_name LIKE '%Quincey'
ORDER BY status ASC, member_name ASC;
```

---

### 📋 Упражнения: Группировка, оператор GROUP BY
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/groupping)

#### Задача 1. Количество комнат по типам
**Условие:** Сгруппируйте данные из таблицы Rooms по полю home_type и выведите тип жилья и количество комнат каждого типа. Используйте псевдоним count_rooms для количества комнат.

```sql
SELECT home_type, COUNT(*) AS count_rooms 
FROM Rooms
GROUP BY home_type;
```

#### Задача 2.  Средняя цена по типу жилья и ТВ
**Условие:** Сгруппируйте данные из таблицы Rooms по полям home_type и has_tv. Выведите тип жилья, признак наличия телевизора (поле has_tv) и среднюю цену для каждой группы. Используйте псевдоним avg_price для средней цены.

```sql
SELECT home_type, has_tv, AVG(price) AS avg_price
FROM Rooms
GROUP BY home_type, has_tv;
```

---

### 📋 Упражнения: Агрегатные функции
**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/aggregate-functions)

#### Задача 1. Группировка и сортировка
**Условие:** Подсчитайте количество учеников в каждом классе, а также отсортируйте их по убыванию количества учеников. Принадлежность ученика к конкретному классу вы можете получить из таблицы Student_in_class. В качестве результата необходимо вывести идентификатор класса (поле class) и количество учеников в этом классе.
Для вывода количества учеников используйте псевдоним count.

```sql
SELECT class, COUNT(*) AS count
FROM Student_in_class
GROUP BY class
ORDER BY count DESC;
```

#### Задача 2.  Агрегатные функции MIN и MAX

**Условие:** Для каждого из существующих статусов (поле status) найдите самого старого человека (используйте поле birthday). Выведите статус и дату рождения.
Для вывода даты рождения используйте псевдоним birthday.

```sql
SELECT status, MIN(birthday) AS birthday
FROM FamilyMembers
GROUP BY status;
```

#### Задача 3.  Агрегатная функция AVG

**Условие:** Получите среднее время полётов, совершённых на каждой из моделей самолёта. Выведите поле plane и среднее время полётов в секундах.
Для вывода времени используйте псевдоним time.
Чтобы получить разницу во времени в секундах между двумя датами используйте:
Для MySQL: TIMESTAMPDIFF(second, time_out, time_in)
Для PostgreSQL: EXTRACT(EPOCH FROM (time_in - time_out))

```sql
SELECT plane, AVG(TIMESTAMPDIFF(second, time_out, time_in)) AS time
FROM Trip
GROUP BY plane;
```

#### Задача 4.  Выборка с использованием нескольких агрегатных функций

**Условие:** Выведите идентификатор комнаты (поле room_id), среднюю стоимость за один день аренды (поле price, для вывода используйте псевдоним avg_price), а также количество резерваций этой комнаты (используйте псевдоним count). Полученный результат отсортируйте в порядке убывания сначала по количеству резерваций, а потом по средней стоимости.

```sql
SELECT room_id, 
       AVG(price) AS avg_price, 
       COUNT(*) AS count
FROM Reservations
GROUP BY room_id
ORDER BY count DESC, avg_price DESC;
```
