# Retornar valores modificados

```sql
-- PostgreSQL

DELETE FROM sessions
WHERE ip = '127.0.0.1'
RETURNING id, user_agent, last_access;
```

<p>Muitas operações de manutenção são baseadas em encontrar linhas particulares, processá-las (por exemplo, enviar um e-mail ou calcular algumas estatísticas) e marcá-las como processadas.

Tipicamente, uma flag dentro da linha é atualizada ou deletada, pois não é mais necessária.

Esse fluxo de trabalho pode ser simplificado usando o recurso `RETURNING` e fazendo a manipulação de dados e seleção dos dados em um único passo.</p>

<p>
Esse recurso está disponível para DELETE , INSERT e UPDATE queries e sempre retornará os dados após a modificação, por exemplo, os dados inseridos ou atualizados com todos os gatilhos executados e valores gerados disponíveis.
</p>

> [!NOTE]  
> Esse recurso está disponível apenas para PostgreSQL.
