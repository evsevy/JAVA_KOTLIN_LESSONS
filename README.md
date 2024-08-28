# SQL Query Parser

Этот проект представляет собой простейший парсер SQL-запросов, написанный на языке Kotlin и Java. 
Он позволяет разобрать SQL-запрос и структурировать различные его компоненты (выбранные колонки, таблицы, условия и т.д.) в удобный для работы формат.

## Описание классов

### Query

Класс `Query` представляет основные компоненты SQL-запроса:

- `columns`: список выбранных колонок
- `fromSources`: список источников данных (таблиц)
- `joins`: список объединений таблиц
- `whereClauses`: условия отбора
- `groupByColumns`: колонки для группировки
- `sortColumns`: колонки для сортировки
- `limit`: лимит на количество возвращаемых строк
- `offset`: сдвиг для возврата строк

#### Методы
- `getColumns()`: возвращает список выбранных колонок.
- `getFromSources()`: возвращает список источников данных.
- `getJoins()`: возвращает список объединений таблиц.
- `getWhereClauses()`: возвращает условия отбора.
- `getGroupByColumns()`: возвращает колонки для группировки.
- `getSortColumns()`: возвращает колонки для сортировки.

### SqlParser

Класс `SqlParser` содержит метод `parse`, который принимает строку SQL-запроса и возвращает объект класса `Query`, содержащий разобранные компоненты. 

#### Алгоритм работы метода `parse`:
1. Удаление лишних пробелов из SQL-запроса.
2. Использование регулярных выражений для извлечения различных компонентов SQL-запроса: 
   - Выбраные колонки (`SELECT`)
   - Источники данных (`FROM`)
   - Условия (`WHERE`)
   - Группировка (`GROUP BY`)
   - Сортировка (`ORDER BY`)
   - Ограничение (`LIMIT` и `OFFSET`)
   - Объединения таблиц (`JOIN`)
3. Обработка (предварительная) подзапросов.

### Пример использования

В методе `main` демонстрируется работа парсера:

kotlin:
fun main() {
    val sql = "SELECT a.id, b.name FROM A a INNER JOIN B b ON a.id = b.a_id WHERE a.status = 1 AND b.count > 100 GROUP BY a.id ORDER BY b.name LIMIT 10 OFFSET 5"

    // Парсим запрос
    val parsedQuery = SqlParser.parse(sql)

    // Выводим результат
    println(parsedQuery)
}


## Установка и запуск

1. Убедитесь, что у вас установлен Java SDK (версия 8 или выше).
2. Склонируйте или загрузите проект на локальное устройство.
3. Откройте проект в вашей среде разработки (например, IntelliJ IDEA).
4. Запустите файл с методом `main`, чтобы протестировать работу парсера.

## Заключение

Данный парсер предназначен для простых SQL-запросов и является хорошим началом для понимания работы с регулярными выражениями и парсингом текстовых данных. 

Меркулов Е. В.
Будущие улучшения могут включать поддержку более сложных запросов, таких как вложенные подзапросы и дополнительные операторы SQL.
