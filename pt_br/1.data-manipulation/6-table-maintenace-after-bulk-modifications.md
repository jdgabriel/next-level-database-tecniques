# Manutenção da tabela após atualização em massa

```sql
-- MySQL
ANALYZE TABLE users;
```

```sql
-- PostgreSQL
ANALYZE SKIP_LOCKED users;
```

<p>
O banco de dados precisa de estatísticas atualizadas sobre suas tabelas, como a quantidade aproximada de linhas, distribuição de dados de valores e mais, para calcular a maneira mais eficiente de executar sua consulta.
</p>
<p>
Ao contrário dos índices, que são alterados automaticamente sempre que uma linha que afeta seus dados é criada, atualizada ou excluída, as estatísticas não são modificadas a cada alteração. Uma recálculo é acionado apenas quando um limite de alterações em uma tabela é ultrapassado.
</p>
<p>
Sempre que você altera uma grande parte de uma tabela, o número de linhas afetadas pode ainda estar abaixo do limite de recálculo de estatísticas, mas significativo o suficiente para tornar as estatísticas incorretas. Algumas consultas podem se tornar muito lentas à medida que o banco de dados prevê o melhor plano de consulta com base nas informações agora incorretas sobre a tabela.
</p>
<p>
Portanto, você deve analisar uma tabela para acionar o recálculo de estatísticas após cada alteração significativa para garantir consultas rápidas.
</p>