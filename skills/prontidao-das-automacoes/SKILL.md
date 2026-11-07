---
name: prontidao-das-automacoes
description: Verifica se as automações do Pontuali estão prontas para funcionar de verdade (ligadas, com janela de envio coerente, com público e dados completos). Use quando o usuário quiser ligar, revisar ou entender as automações.
---

# Prontidão das automações

Siga a skill `pontuali-operador`. Este acesso é de leitura: você diagnostica e recomenda; ligar ou ajustar é feito no app.

## Passo a passo
1. `list_automations`: para cada automação, veja se está ligada, a janela de envio (`sendFrom`/`sendUntil`) e o modo de público.
2. Para cada automação ligada, `get_automation_audience` (primeira página): estime quantos contatos serão alcançados e os principais `whyNotCovered`.
3. `list_contacts` (uma ou duas páginas) para checar se a base tem telefone e, para aniversário, data de nascimento (campo `birthdayMonthDay` vazio = faltando).
4. `get_workspace_overview` para confirmar o perfil e os canais.

## Diagnóstico por automação
| Situação | Recomendação |
|---|---|
| Desligada, mas com público grande | Perguntar se é intencional; indicar onde ligar no app |
| Ligada, janela muito curta ou fora do horário comercial | Sugerir revisar a janela |
| Ligada, mas a maioria do público está excluída | Mostrar o motivo mais comum e como corrigir |
| Ligada e saudável | Confirmar e sugerir acompanhar semanalmente |

## Cuidados
- Opt-out prevalece sobre qualquer configuração: não sugira "forçar" envio.
- Não prometa resultados (taxa de resposta, receita). Fale só do que os dados mostram.
