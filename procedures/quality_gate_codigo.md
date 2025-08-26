# Quality Gate de Código (v1.0)
**Objetivo:** Estabelecer critérios mínimos de qualidade em CI.
**Escopo:** Revisões e merges para branches principais.
**Entrada:** Pipeline configurado, projeto versionado.
**Saída:** Build falha ao violar critérios críticos.
**Owner:** Responsável técnico

## Passo a passo
1) Definir regras (smells críticos, cobertura, formatação).
   - Evidência: relatório do pipeline
   - Rollback: afrouxar regras num branch de hotfix com justificativa
2) Implementar checks automáticos na pipeline.
   - Evidência: artefatos de CI (logs, relatórios)
   - Rollback: desativar job específico temporariamente

## Critérios de aceite
- Build falha em violações críticas
- Relatórios acessíveis e versionados

## Evidências
- Caminho: evidence/plataforma_ci/<case>/
- Itens: métricas, prints, JSONs, logs
