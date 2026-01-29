# 📖 Модуль 3. Многотабличные запросы

## Урок 1. Многотабличные запросы, JOIN

### 💡 Ключевые моменты:

- **JOIN** объединяет таблицы по связующим полям
- **ON** задаёт условие связи
- Желательно использовать псевдонимы для читаемости
- Всегда нужно указывать таблицу для полей

### Общая структура многотабличного запроса

```sql
SELECT поля_таблиц
FROM таблица_1
[INNER] | [[LEFT | RIGHT | FULL][OUTER]] JOIN таблица_2
    ON условие_соединения
[[INNER] | [[LEFT | RIGHT | FULL][OUTER]] JOIN таблица_n
    ON условие_соединения]
```

### Базовый пример
```sql
-- Без псевдонимов
SELECT member_name, amount * unit_price AS price
FROM Payments
INNER JOIN FamilyMembers
    ON Payments.family_member = FamilyMembers.member_id;

-- С псевдонимами (рекомендуется)
SELECT fm.member_name, pay.amount * pay.unit_price AS price
FROM Payments AS pay
INNER JOIN FamilyMembers AS fm
    ON pay.family_member = fm.member_id;
```
