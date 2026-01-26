### 📋 Упражнения: Базовый синтаксис SELECT

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

