### 1. Добавление нового товара

Добавьте новый товар в таблицу `Goods` с именем `'Table'` и типом `'equipment'`.  
В качестве первичного ключа (`good_id`) укажите количество записей в таблице + 1.

```sql
INSERT INTO Goods (good_id, good_name, type)
SELECT
    (SELECT COUNT(*) + 1 FROM Goods),
    'Table',
    good_type_id
FROM GoodTypes
WHERE good_type_name = 'equipment';
```
