## 📋 Упражнения: Базовый синтаксис SELECT

### Задача 1. Вывод строки
**Условие:** С помощью оператора SELECT выведите текст "Hello world"

SELECT 'Hello world';
```

### Задача 2. SELECT по всем столбцам
**Условие:** Выведите все столбцы из таблицы Payments.

```sql
SELECT *
FROM Payments;
```

### Задача 3. SELECT по нескольким столбцам
**Условие:** Выведите поля member_id, member_name и status из таблицы FamilyMembers.

```sql
SELECT member_id, member_name, status
FROM FamilyMembers;
```

### Задача 4. Вывод с псевдонимами
**Условие:** Выведите поле name из таблицы Passenger. При выводе данного поля используйте псевдоним "passengerName"

```sql
SELECT name AS passengerName
FROM Passenger;
```
