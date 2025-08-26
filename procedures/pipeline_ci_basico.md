# Pipeline CI Básico (agnóstico) (v1.0)
**Objetivo:** Executar validações mínimas de forma reprodutível.
**Escopo:** Projetos com build/test/lint.
**Entrada:** Definição de build, testes e lint.
**Saída:** Pipeline executável com estágios validate/test/package.
**Owner:** Responsável técnico

## Passo a passo
1) Definir estágios e comandos mínimos por linguagem.
   - Evidência: artefatos do pipeline
   - Rollback: reverter alterações no arquivo de pipeline
2) Habilitar cache e relatórios de teste/lint.
   - Evidência: tempo de pipeline e relatórios
   - Rollback: desativar caches ou etapas problemáticas

## Critérios de aceite
- Pipeline reproduzível e determinístico
- Relatórios de teste disponíveis

## Evidências
- Caminho: evidence/plataforma_ci/<case>/
- Itens: métricas, prints, JSONs, logs
