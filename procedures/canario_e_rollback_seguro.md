# Canário e Rollback Seguro (v1.0)
**Objetivo:** Reduzir risco de releases com canário e rollback testado.
**Escopo:** Implantações em produção.
**Entrada:** Ambiente preparado e métricas de baseline.
**Saída:** Release gradual com rollback ensaiado.
**Owner:** Responsável SRE

## Passo a passo
1) Planejar canário (segmento/percentual/tempo) e métricas de go/no-go.
   - Evidência: planilha de critérios e métricas de baseline
   - Rollback: procedimento de rollback manual validado
2) Executar canário, monitorar e decidir go/no-go.
   - Evidência: gráficos e logs do período de canário
   - Rollback: rollback automatizado ou manual em playbook

## Critérios de aceite
- Sem degradação significativa nas métricas-chave
- Rollback validado em DRY-RUN recente

## Evidências
- Caminho: evidence/sre/<case>/
- Itens: métricas, prints, JSONs, logs
