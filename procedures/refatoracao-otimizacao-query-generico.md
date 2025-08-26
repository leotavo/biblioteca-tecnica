# procedures/refatoracao-otimizacao-query-generico.md

## Otimização de Query: Validação Funcional + Métrica no Frontend (v1.1)

**Objetivo**  
Assegurar que qualquer otimização de consulta preserve a funcionalidade e resulte em desempenho igual ou melhor percebido no frontend.

**Escopo**  
- Queries SQL/NoSQL utilizadas em endpoints de backend.  
- Páginas/telas do frontend que consomem esses endpoints.  
- Aplicável a múltiplas demandas de otimização.

**Entrada**  
- Ticket/issue da demanda.  
- Endpoint(s) afetados.  
- Página(s)/tela(s) afetadas.  
- Query baseline e versão otimizada.

**Saída**  
- Evidências de paridade funcional (texto).  
- Evidências de performance no frontend (texto + screenshots).  
- Comparativo baseline vs otimizada.  
- Registro de decisão (Go/No-Go).

**Owner**  
Leonardo Trindade

---

### Passo a Passo

1. **Fixar baseline**  
   - Coletar métricas atuais de API (latência, erro%).  
   - Coletar métricas de frontend (tempo até dados visíveis, interação crítica).  
   - Evidência: `evidence/refatoracao/<case>/baseline/metrics_api.json`  
   - Evidência: `evidence/refatoracao/<case>/baseline/screenshots/`  
   - Rollback: N/A.

2. **Congelar cenário de dados**  
   - Selecionar dataset e parâmetros fixos (filtros, ordenação, paginação).  
   - Evidência: `evidence/refatoracao/<case>/dataset/contexto.md`  
   - Rollback: N/A.

3. **Executar versão otimizada**  
   - Implantar a query otimizada em homologação.  
   - Evidência: `evidence/refatoracao/<case>/setup/implante.txt`  
   - Rollback: reimplantar baseline.

4. **Validar paridade funcional (obrigatório)**  
   - Comparar payload baseline vs otimizada: schema, count, ordenação, paginação, agregações.  
   - Evidência: `evidence/refatoracao/<case>/paridade/api_diff.json`  
   - Rollback: reimplantar baseline.

5. **Medição de performance (obrigatório)**  
   - API: rodar requisições repetidas em baseline e otimizada.  
   - Frontend: medir tempo até dados visíveis e interação crítica (filtrar/ordenar/paginar).  
   - Evidência:  
     - `evidence/refatoracao/<case>/perf/api_metrics.json`  
     - `evidence/refatoracao/<case>/perf/frontend_metrics.json`  
     - `evidence/refatoracao/<case>/screenshots/`  
   - Rollback: N/A.

6. **Checagens de observabilidade (opcional)**  
   - Monitorar logs, erros, consumo de CPU/IO no DB/pods durante testes.  
   - Evidência: `evidence/refatoracao/<case>/observabilidade/notas.md`  
   - Rollback: N/A.

7. **Revisão de plano de execução (opcional)**  
   - Executar `EXPLAIN/ANALYZE` para comparar baseline vs otimizada.  
   - Evidência: `evidence/refatoracao/<case>/db/plan_diff.txt`  
   - Rollback: N/A.

8. **Consolidar decisão (Go/No-Go)**  
   - Comparar baseline vs otimizada.  
   - Critérios:  
     - Funcionalmente idêntica.  
     - Performance otimizada igual ou melhor que baseline.  
     - Registrar ganhos mensuráveis quando houver.  
   - Evidência: `evidence/refatoracao/<case>/decisao/resultado-final.md`  
   - Rollback: reimplantar baseline.

---

### Critérios de Aceite
- Resultados funcionais idênticos entre baseline e otimizada.  
- Performance da otimizada **igual ou superior** à baseline.  
- Ganhos observados destacados (quando houver).  
- Evidências salvas em texto + screenshots.  
- Rollback documentado (reimplantar baseline).

---

### Notas/Aprendizados
- Screenshots obrigatórios: carregamento inicial + uma interação crítica.  
- Métricas de infraestrutura e revisão de planos de execução são opcionais.  
- Procedimento replicável para qualquer demanda de otimização de query.
