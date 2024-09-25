                                           
# Mission 3

## Показываю данные в supabase,работу buildship workflows и sql-запросы из части 3.

[Link to video](https://disk.yandex.ru/i/H_Mw9GluVTtrGg)

## SQL-запросы

### Запрос 1: Список юзернеймов пользователей
```sql
SELECT username
FROM users;
```
### Запрос 2: Количество отправленных сообщений каждым пользователем
```sql
SELECT users.username, COUNT(messages.id) AS number_of_sent_messages
FROM messages
JOIN users ON users.id = messages.from
GROUP BY users.username;
```
### Запрос 3: Пользователь с наибольшим количеством полученных сообщений
```sql
SELECT users.username, COUNT(messages.id) AS number_of_received_messages
FROM messages
JOIN users ON users.id = messages.to
GROUP BY users.username
ORDER BY number_of_received_messages DESC
LIMIT 1;
```
### Запрос 4: Среднее количество отправленных сообщений каждым пользователем
```sql 
SELECT AVG(sent_messages_count) AS average_sent_messages
FROM (
    SELECT COUNT(messages.id) AS sent_messages_count
    FROM messages
    JOIN users ON users.id = messages.from
    GROUP BY users.username
) AS message_counts;
```

 
