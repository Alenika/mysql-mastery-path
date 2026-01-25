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
