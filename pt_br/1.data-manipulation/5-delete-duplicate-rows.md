# Excluir linhas duplicadas

```sql
-- MySQL

WITH duplicates AS (
  SELECT id, ROW_NUMBER() OVER(
    PARTITION BY firstname, lastname, email
    ORDER BY age DESC
  ) AS rownum
    FROM contacts
)
DELETE contacts
FROM contacts
JOIN duplicates USING(id)
WHERE duplicates.rownum > 1;
```
```sql
-- PostgreSQL

WITH duplicates AS (
  SELECT id, ROW_NUMBER() OVER(
      PARTITION BY firstname, lastname, email
    ORDER BY age DESC
  ) AS rownum
  FROM contacts
)
DELETE FROM contacts
USING duplicates
WHERE contacts.id = duplicates.id AND duplicates.rownum > 1;
```

> [!NOTE]  
> Eu escrevi um texto mais extenso sobre este tópico em meu site focado em banco de dados SqlForDevs.com: Excluir Linhas Duplicadas. [Delete Duplicate Rows](https://sqlfordevs.com/delete-duplicate-rows)