# Refatoração Backend (Java) (v1.0)
**Objetivo:** Reduzir complexidade e dívidas de código mantendo comportamento.
**Escopo:** Código de backend; não cobre mudanças de contrato externo.
**Entrada:** Código alvo, testes existentes, dados de métricas.
**Saída:** Código mais coeso, testes passando, métricas antes/depois.
**Owner:** Responsável técnico

## Passo a passo
1) Mapear hotspots e criar testes de caracterização (Golden Master).
   - Evidência: antes/depois de complexidade e cobertura
   - Rollback: reverter commit / desfazer mudanças
2) Aplicar extração de métodos/objetos, remover N+1, ajustar Hikari.
   - Evidência: latência p95 e dif de code smells
   - Rollback: desligar feature flag / rollback de release

## Critérios de aceite
- Complexidade média reduzida nas áreas tocadas
- Cobertura ≥ 70% e latência p95 não piora

## Evidências
- Caminho: evidence/refatoracao/<case>/
- Itens: métricas, prints, JSONs, logs
