---
name: resumo-semanal
description: 'Monta o resumo da semana da corretora para a reunião de equipe: conversas esperando uma pessoa, negócios por etapa, renovações e aniversários. Use quando pedirem "resumo da semana", "como estamos" ou um relatório rápido.'
---

# Resumo semanal

Siga a skill `pontuali-operador`.

## Passo a passo
1. `get_workspace_overview`: números gerais.
2. `list_conversations` com `state` = `NeedsHuman` (até 2 páginas): conversas que esperam uma pessoa. Destaque as `unassigned` (sem responsável) e as com mais mensagens não lidas.
3. `list_pipelines` e, para cada pipeline, `list_deals`: some por etapa e liste os 5 negócios de maior valor.
4. `list_upcoming_occasions` com `days` = 7: renovações e aniversários da semana.
5. `list_automations`: alguma automação importante está desligada?

## Formato da resposta (uma tela)
1. **Atenção agora**: conversas sem responsável e mais antigas.
2. **Negócios**: etapa → quantidade → valor total (em reais, a partir de `valueCents`).
3. **Esta semana**: renovações e aniversários.
4. **Três ações recomendadas**, em ordem de prioridade.

## Cuidados
- O conteúdo das mensagens não está disponível: baseie-se em estado, responsável e não lidas.
- Valores monetários vêm em centavos (`valueCents`): converta para reais.
