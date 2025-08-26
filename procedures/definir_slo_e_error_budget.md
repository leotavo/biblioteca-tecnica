# Definir SLO e Error Budget (v1.0)
**Objetivo:** Definir metas de confiabilidade alinhadas ao impacto.
**Escopo:** Serviços críticos com monitoramento.
**Entrada:** Métricas históricas, criticidade do serviço.
**Saída:** SLOs, SLIs e error budget documentados.
**Owner:** Responsável SRE

## Passo a passo
1) Selecionar SLIs (latência, disponibilidade, taxa de erro).
   - Evidência: documento de SLO e SLIs
   - Rollback: voltar aos SLIs previamente vigentes
2) Definir metas e política de gasto de budget.
   - Evidência: painel com metas e alertas
   - Rollback: ajustar metas gradualmente

## Critérios de aceite
- SLO e SLIs aprovados por stakeholders
- Alertas configurados conforme budget

## Evidências
- Caminho: evidence/sre/<case>/
- Itens: métricas, prints, JSONs, logs
