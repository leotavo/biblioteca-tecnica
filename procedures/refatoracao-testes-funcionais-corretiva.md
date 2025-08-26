# procedures/refatoracao-testes-funcionais-corretiva.md

## Testes Funcionais – Demanda Corretiva (v1.0)

**Objetivo**  
Garantir que a correção implementada resolve o defeito reportado, sem introduzir regressões.

**Escopo**  
Aplicável a demandas corretivas em sistemas internos (backend, frontend ou integrações).  

**Entrada**  
- Ticket ou chamado com descrição do defeito.  
- Branch de correção em ambiente de homologação.  
- Plano de testes ou casos de teste derivados do defeito.  

**Saída**  
- Evidências de testes bem-sucedidos.  
- Registro de aprovação/reprovação da correção.  

**Owner**  
Leonardo Trindade  

---

### Passo a Passo

1. **Preparar ambiente de testes**  
   - Garantir que a versão com correção está em homologação.  
   - Evidência: print/registro de versão implantada em `evidence/refatoracao/<case>/ambiente.txt`  
   - Rollback: restaurar versão anterior via pipeline/deploy.

2. **Reproduzir defeito na versão anterior (se possível)**  
   - Validar que o erro de fato ocorria antes da correção.  
   - Evidência: print/log do erro em `evidence/refatoracao/<case>/defeito-anterior.log`  
   - Rollback: não aplicável.

3. **Executar caso de teste da correção**  
   - Seguir o roteiro definido no ticket.  
   - Evidência: captura de tela ou log em `evidence/refatoracao/<case>/teste-correcao.log`  
   - Rollback: desfazer a ação no sistema (ex.: excluir registro de teste).

4. **Executar testes de regressão mínima**  
   - Validar funcionalidades relacionadas.  
   - Evidência: checklist assinado em `evidence/refatoracao/<case>/regressao-checklist.md`  
   - Rollback: restaurar base de dados, se alterada.

5. **Registrar resultado final**  
   - Aprovar/reprovar a correção.  
   - Evidência: parecer salvo em `evidence/refatoracao/<case>/resultado-final.md`  
   - Rollback: abrir novo ticket, se falha persistir.

---

### Critérios de Aceite
- O defeito original não ocorre mais.  
- Funcionalidades relacionadas continuam operando.  
- Todas as evidências estão salvas nos caminhos definidos.  
- Rollback documentado e testável.  

---

### Notas/Aprendizados
- Sempre versionar evidências em repositório de homologação.  
- Criar checklist mínimo de regressão por módulo para padronizar.  
