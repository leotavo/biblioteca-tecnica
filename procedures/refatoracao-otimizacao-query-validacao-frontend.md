# procedures/refatoracao-otimizacao-query-validacao-frontend.md

## Otimização de Query: Validação Funcional + Métrica no Frontend (v1.0)

**Objetivo**  
Garantir que a query otimizada mantém o comportamento funcional e melhora a performance observada no frontend.

**Escopo**  
- Backends com endpoints que dependem de consultas SQL/NoSQL.  
- Medição de impacto em páginas/telas do frontend que consomem esses endpoints.

**Entrada**  
- Ticket/issue da otimização (<case>).  
- Endpoint(s) alvo (<endpoint>) e tela/página afetada (<pagina>).  
- Query atual (baseline) e proposta otimizada (flagável/parametrizável).

**Saída**  
- Evidências de **paridade funcional** (resultado idêntico).  
- Comparativo de **performance** API e frontend (baseline vs otimizada).  
- Go/No-Go documentado.

**Owner**  
Leonardo Trindade

---

### Passo a Passo

1. **Fixar baseline (antes da otimização)**
   - Coletar métricas de API: p50/p95/p99, TTFB, payload size, erro (%).  
   - Coletar métricas de frontend na <pagina>: FCP/LCP/INP (ou métricas visuais equivalentes), tempo de carregamento dos dados, FPS em renderização de listas (quando aplicável).  
   - Evidência: `evidence/refatoracao/<case>/baseline/metrics_api.json`, `.../metrics_frontend.json`  
   - Rollback: N/A.

2. **Congelar cenário de dados para comparação**
   - Selecionar dataset estável (fixtures ou snapshot) e parâmetros idênticos (filtros/ordenação/paginação).  
   - Evidência: `evidence/refatoracao/<case>/dataset/contexto.md`  
   - Rollback: N/A.

3. **Habilitar execução lado a lado (baseline vs otimizada)**
   - Introduzir **feature flag** / parâmetro (`?strategy=optimized`) em homologação para alternar a query.  
   - Garantir logs com `traceId` e marcação da estratégia.  
   - Evidência: `evidence/refatoracao/<case>/setup/flag-config.md`  
   - Rollback: desabilitar flag e retornar ao baseline.

4. **Validar paridade funcional (API)**
   - Executar o mesmo request contra baseline e otimizada.  
   - Comparar: schema, count total, paginação (itens/offset/hasNext), ordenação, campos nulos, agregações.  
   - Usar **comparação determinística** (ex.: checksum por linha/campo) e diffs tolerância zero.  
   - Evidência: `evidence/refatoracao/<case>/paridade/api_diff.json` (vazio/igual = ok)  
   - Rollback: se houver diffs, pausar rollout e abrir sub-issue.

5. **Revisar plano/estratégia da query**
   - Comparar `EXPLAIN`/`EXPLAIN ANALYZE` (custos, índices, cardinalidade, scans).  
   - Evidência: `evidence/refatoracao/<case>/db/plan_baseline.txt`, `.../plan_optimized.txt`  
   - Rollback: reverter hints/índices experimentais.

6. **Medição de performance de API (A/B)**
   - Rodar N requisições por variação (ex.: N=50), registrar p50/p95/p99, TTFB, erro%.  
   - Evidência: `evidence/refatoracao/<case>/perf/api_ab_run.csv`, `.../api_ab_summary.md`  
   - Rollback: N/A.

7. **Medição de performance no frontend**
   - Na <pagina>, medir: tempo até dados visíveis, LCP (quando relevante), tempo de render da lista, interações críticas (ex.: ordenar/filtrar/paginar).  
   - Repetir cenário (3–5 execuções por variação) e calcular média/p95.  
   - Evidência: `evidence/refatoracao/<case>/perf/frontend_ab_run.csv`, `.../frontend_ab_summary.md`  
   - Rollback: N/A.

8. **Checagens de observabilidade**
   - Verificar logs, erros, timeouts, consumo de CPU/IO no DB durante testes.  
   - Evidência: `evidence/refatoracao/<case>/observabilidade/notas.md`  
   - Rollback: N/A.

9. **Comparar e decidir (Go/No-Go)**
   - Consolidar **baseline vs otimizada** (API + frontend).  
   - Se aceitar: documentar thresholds atingidos e plano de rollout.  
   - Evidência: `evidence/refatoracao/<case>/decisao/resultado-final.md`  
   - Rollback: plano de reversão (desligar flag; reimplantar baseline).

---

### Critérios de Aceite (defaults)
- **Paridade funcional 100%** (sem diffs no payload e no comportamento de paginação/ordenação).  
- **API**: p95 **≤ -20%** vs baseline; erro% **≤ baseline**.  
- **Frontend**: LCP (ou tempo até dados visíveis) **≤ -10%** vs baseline; interações críticas **≤ -15%**.  
- **DB**: custo estimado/tempo médio do plano **≤ -15%** vs baseline.  
- Evidências completas nos caminhos definidos e rollback operacional.

---

### Notas/Aprendizados
- Padronize o comparador de payload (normalização de ordem, precisão numérica e datas).  
- Prefira **flags** a branches long-lived para facilitar teste A/B controlado.
