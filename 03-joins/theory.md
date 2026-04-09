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
## Урок 2. Внутреннее соединение INNER JOIN

```sql
SELECT поля_таблиц
FROM таблица_1
[INNER] JOIN таблица_2
    ON условие_соединения
[[INNER] JOIN таблица_n
    ON условие_соединения]
```

## Урок 3. Внешнее соединение OUTER JOIN

```sql
SELECT *
FROM левая_таблица
LEFT JOIN правая_таблица
   ON правая_таблица.ключ = левая_таблица.ключ

UNION ALL

SELECT *
FROM левая_таблица
RIGHT JOIN правая_таблица
ON правая_таблица.ключ = левая_таблица.ключ
 WHERE левая_таблица.ключ IS NULL
```

## Урок 4. Ограничение выборки, оператор LIMIT

```sql
SELECT поля_выборки
FROM список_таблиц
LIMIT [количество_пропущенных_записей,] количество_записей_для_вывода;
```

```sql
SELECT поля_выборки
FROM список_таблиц
LIMIT количество_записей_для_вывода [OFFSET количество_пропущенных_записей];
```

## Урок 5. Подзапросы

- **Подзапрос** — это запрос, использующийся в другом SQL запросе. 
- **Подзапрос** всегда заключён в круглые скобки и обычно выполняется перед основным запросом.

## Урок 6. Подзапрос с одной строкой с одним столбцом

**Скалярный подзапрос** — это подзапрос, который возвращает ровно одну строку и один столбец. 
Его часто используют в `WHERE` с операторами сравнения (`=`, `<>`, `>`, `<`), а также в `SELECT` как отдельное вычисляемое значение.

```sql
SELECT
    (SELECT name FROM company LIMIT 1) AS company_name;
```

## Урок 7. Подзапросы с несколькими строками и одним столбцом

**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/subquery-with-one-column-several-row)

Если подзапрос возвращает более одной строки, его нельзя использовать с простыми операторами сравнения (`=`, `<>` и т.д.).  
Для таких подзапросов используются 3 специальных оператора:

| Оператор | Возвращает TRUE если... |
|----------|------------------------|
| `ALL`    | условие верно **для всех** значений из набора |
| `ANY`    | условие верно **хотя бы для одного** значения из набора |
| `IN`     | значение **входит** в набор |

---

### Оператор ALL

Сравнивает значение с **каждым** элементом набора. TRUE — только если все сравнения вернули TRUE.

```sql
-- Проверка: все ли комнаты дешевле 200?
SELECT 200 > ALL(SELECT price FROM Rooms);
```

```sql
-- Найти владельцев жилья, которые НИКОГДА сами не снимали жильё
SELECT DISTINCT name
FROM Users
INNER JOIN Rooms ON Users.id = Rooms.owner_id
WHERE Users.id <> ALL (
    SELECT DISTINCT user_id FROM Reservations
);
```

> 💡 `<> ALL` — это аналог `NOT IN`, но безопаснее при наличии `NULL` в подзапросе.

---

### Оператор IN

Проверяет, входит ли значение в список результатов подзапроса.

```sql
-- Найти всех владельцев жилья стоимостью >= 150
SELECT * FROM Users
WHERE id IN (
    SELECT DISTINCT owner_id FROM Rooms WHERE price >= 150
);
```

---

### Оператор ANY

Возвращает TRUE, если хотя бы одно сравнение из набора истинно. `= ANY` эквивалентен `IN`.

```sql
-- Найти пользователей, у которых есть хотя бы 1 жильё стоимостью > 150
SELECT * FROM Users
WHERE id = ANY (
    SELECT DISTINCT owner_id FROM Rooms WHERE price >= 150
);
```

---

### 💡 Сравнение операторов

```sql
-- Эти два запроса эквивалентны:
WHERE id IN (SELECT owner_id FROM Rooms WHERE price >= 150)
WHERE id = ANY (SELECT owner_id FROM Rooms WHERE price >= 150)

-- А эти два — тоже эквивалентны:
WHERE id NOT IN (SELECT user_id FROM Reservations)
WHERE id <> ALL (SELECT user_id FROM Reservations)
```

## Урок 8. Подзапросы с несколькими столбцами (многостолбцовые)

**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/subquery-with-several-column)

Подзапрос может возвращать **несколько столбцов и строк** (производную таблицу). Тогда сравниваем **пары/множества значений**.

### Синтаксис сравнения по нескольким столбцам

```sql
SELECT ...
FROM таблица
WHERE (столбец1, столбец2) IN (
    SELECT столбецA, столбецB FROM подзапрос
);
```

**IN** сравнивает **попарно** — ищет точное совпадение кортежей.

### 🔍 Пример: бронирования с неизменной ценой

**Задача:** найти бронирования, где цена на момент брони (`Reservations.price`) = текущей цене комнаты (`Rooms.price`).

```sql
SELECT * FROM Reservations
WHERE (room_id, price) IN (
    SELECT id, price FROM Rooms
);
```

**Логика:**
1. Подзапрос → таблица `(id, price)` всех комнат
2. Основной запрос фильтрует бронирования, где пара `(room_id, price)` есть в этой таблице

**Альтернатива через JOIN** (более читаемо):
```sql
SELECT Reservations.*
FROM Reservations
INNER JOIN Rooms ON Reservations.room_id = Rooms.id
WHERE Reservations.price = Rooms.price;
```

### 💡 Ключевые отличия

| Подзапросы | 1 столбец | 2+ столбца |
|------------|-----------|------------|
| **Оператор** | `IN`, `ANY`, `ALL` | `IN` (кортежи) |
| **Пример** | `id IN (SELECT id...)` | `(id, price) IN (SELECT id, price...)` |
| **Когда использовать** | Список ID | Пары/множества значений |

### ⚠️ Ограничения
- Количество столбцов **должно совпадать**
- `NOT IN` осторожно — ломается на NULL
- Лучше `LEFT JOIN ... IS NULL` для "не существует"

## Урок 9. Коррелированные подзапросы

**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/correlated-subqueries)

### 🔗 Что такое коррелированный подзапрос?

**Коррелированный** = **"связанный"** — подзапрос **ссылается на столбцы внешнего (основного) запроса**.

**Некоррелированный** (до этого):
```sql
-- Выполняется ОДИН раз
WHERE id IN (SELECT id FROM другая_таблица);
```

**Коррелированный** (новое):
```sql
-- Выполняется для КАЖДОЙ строки внешнего запроса!
SELECT name, (
    SELECT SUM(...) 
    FROM payments 
    WHERE payments.member_id = FamilyMembers.member_id  -- ← ссылка на внешний!
) AS total
FROM FamilyMembers;
```

### 💰 Пример: сколько потратил каждый член семьи

```sql
SELECT FamilyMembers.member_name, (
    SELECT SUM(Payments.unit_price * Payments.amount)
    FROM Payments
    WHERE Payments.family_member = FamilyMembers.member_id  -- Корреляция!
) AS total_spent
FROM FamilyMembers;
```

## Урок 10. Объединение запросов (UNION)

**Источник:** [sql-academy.org](https://sql-academy.org/ru/guide/combining-queries)

Объединяет **результаты 2+ SELECT** в **одну таблицу**. 

### 🎯 Синтаксис

```sql
SELECT поля FROM таблицы1 WHERE ...
UNION [ALL]
SELECT поля FROM таблицы2 WHERE ...;
```

**UNION** vs **JOIN**:
| UNION | JOIN |
|-------|------|
| Объединяет **результаты запросов** | Объединяет **строки таблиц** |
| Независимые SELECT | Связанные таблицы |
| Вертикальное объединение | Горизонтальное |

### ⚙️ Модификаторы

- **`UNION`** — **убирает дубликаты** (DISTINCT по умолчанию)
- **`UNION ALL`** — **оставляет все** (быстрее)
