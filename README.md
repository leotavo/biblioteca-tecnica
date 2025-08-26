# 📚 Playbooks, Fluxos e Procedimentos Replicáveis

Repositório para **padronizar e replicar** fluxos, procedimentos (SOPs) e templates da atuação profissional — agnóstico de stack e **pronto para futura automação** com versões humana (Markdown) e máquina (YAML).

## Objetivo
- Tornar **repetível** o que funciona (fluxos, SOPs, checklists).
- Aumentar **previsibilidade** e **rastreabilidade** com critérios de aceite e evidências.
- Permitir automação incremental por **schema YAML** e módulos de CI.

## Estrutura
```
.
├─ README.md
├─ catalog/
├─ flows/{ mermaid/, bpmn/ }
├─ procedures/            # humano (MD)
├─ procedures_machine/    # máquina (YAML)
├─ schemas/
├─ templates/{ issues/, merge_requests/, docs/ }
├─ evidence/{ refatoracao/, plataforma_ci/, sre/ }
├─ governance/
└─ automation/{ ci_modules/, scripts/ }
```

## Convenções
- **Sem segredos** no repositório.
- Cada procedimento possui duas versões: `procedures/*.md` e `procedures_machine/*.yaml`.
- Evidências vão para `evidence/<tema>/<case>/...`.
