# Prevenção de bloqueio de atualizações em linhas acessadas

```sql
-- MySQL

INSERT INTO tweet_statistics ( 
  tweet_id, fanout, likes_count 
) VALUES ( 
  1475870220422107137, FLOOR(RAND() * 10), 1 
) ON DUPLICATE KEY UPDATE likes_count = likes_count + VALUES(likes_count);
```

```sql
-- PostgreSQL

INSERT INTO tweet_statistics (
 tweet_id, fanout, likes_count
) VALUES (
 1475870220422107137, FLOOR(RANDOM() * 10), 1
) ON CONFLICT (tweet_id, fanout) DO UPDATE SET likes_count =
 tweet_statistics.likes_count + excluded.likes_count;
```

<p>
Em algumas aplicações, contadores para, por exemplo, curtidas de um tweet são constantemente atualizados. Durante um pico de tráfego ou para conteúdo em alta, um contador pode ser atualizado inúmeras vezes em um segundo. Devido ao controle de concorrência do banco de dados, as atualizações começarão a interferir umas com as outras, pois uma linha só pode ser bloqueada por uma transação (consulta) de cada vez. Cada atualização será executada uma após a outra, em vez de execução paralela para linhas independentes.
</p>

<p>
Em vez de atualizar uma única linha, os incrementos são distribuídos para, por exemplo, 100 linhas diferentes em uma tabela de contadores especial. O fator de escalonamento agora aumenta pelo número de linhas adicionais que o contador é escrito. Esses valores são posteriormente agregados a um único valor e salvos em sua coluna original que teria tido contenção de bloqueio.
</p>