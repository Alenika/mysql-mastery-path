# 📖 Модуль 2. Основы выборки I

## Урок 1. Базовый синтаксис **SELECT**

**Шаблон запроса:**
```sql
SELECT column_list
FROM table_name;
```
**4 примера:**

1. **Произвольная строка:**
```sql
SELECT 'Hello world';
```

2. **Все колонки таблицы:**
```sql
SELECT *
FROM FamilyMembers;
```

3. **Конкретные колонки:**
```sql
SELECT 
    member_id, 
    member_name 
FROM FamilyMembers;
```

4. **С псевдонимом (AS):**
```sql
SELECT 
    member_name AS Name
FROM FamilyMembers;
```



