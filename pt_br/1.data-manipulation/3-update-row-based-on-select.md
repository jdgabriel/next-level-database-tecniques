# Update baseado em Select

```sql
-- MySQL

UPDATE products
JOIN categories USING(category_id)
SET price = price_base - price_base * categories.discount;
```

```sql
-- PostgreSQL

UPDATE products
SET price = price_base - price_base * categories.discount
FROM categories
WHERE products.category_id = categories.category_id;
```

<p>As tabelas muitas vezes não são atualizadas isoladamente, mas os valores são atualizados com base em informações armazenadas em outras tabelas. Por exemplo, ao aplicar desconto em todos os produtos na Black Friday, um desconto para cada categoria de produto será aplicado. Em vez da abordagem ingênua de executar uma consulta de atualização para cada categoria, você pode atualizar os produtos juntando-os às suas categorias. A junção manual na aplicação é substituída por uma mais eficiente pelo banco de dados.</p>

> [!NOTE]  
> Eu escrevi um texto mais extenso sobre este tópico no meu site focado em banco de dados SqlForDevs.com: [UPDATE from a SELECT](https://sqlfordevs.com/update-from-select)
