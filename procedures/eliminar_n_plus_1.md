# Eliminar N+1 em consultas (v1.0)
**Objetivo:** Eliminar padrões N+1 para reduzir latência e carga no DB.
**Escopo:** Leituras em serviços com ORM.
**Entrada:** Query atual, entidades relacionadas, métricas de DB.
**Saída:** Consulta otimizada com fetch adequado e paginação.
**Owner:** Responsável técnico

## Passo a passo
1) Identificar endpoints com alto número de queries por requisição.
   - Evidência: contagem de queries por requisição
   - Rollback: voltar para consulta original
2) Aplicar fetch join/entity graph e projeções DTO com paginação.
   - Evidência: latência e consumo de CPU/IO do DB
   - Rollback: desabilitar otimizações e revalidar

## Critérios de aceite
- Queda mensurável na contagem de queries
- Latência p95 menor ou estável

## Evidências
- Caminho: evidence/refatoracao/<case>/
- Itens: métricas, prints, JSONs, logs
