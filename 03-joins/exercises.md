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
