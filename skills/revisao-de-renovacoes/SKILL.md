---
name: revisao-de-renovacoes
description: Revisa as apólices que vencem em breve e monta um plano de contato por semana, respeitando quem pediu para não receber mensagens. Use quando o usuário perguntar sobre renovações, vencimentos ou "quem preciso procurar este mês".
---

# Revisão de renovações

Siga a skill `pontuali-operador` (dados mascarados, somente leitura).

## Passo a passo
1. `get_workspace_overview` para ver quantas renovações vencem em 30 dias (`renewalsDueIn30Days`).
2. `list_upcoming_occasions` com `days` = 30 (ou o período que o usuário pedir, no máximo 62). Fique só com os itens de tipo `renewal`.
3. Para cada contato dos primeiros 15 itens, chame `get_contact` e anote o `consent`. Se for `OptedOut`, **não** inclua no plano de contato: liste à parte como "não contatar".
4. Se o usuário quiser detalhes da apólice (seguradora, ramo, vencimento), use `list_records` com `type` = `policy` e `dueBefore`.
5. Confira se a automação de aviso de renovação está ativa com `list_automations` (código `renewal_notice`) e diga isso no final.

## Formato da resposta
- Uma tabela por semana: **Nome | Vencimento | Seguradora/ramo | Situação do consentimento**.
- Abaixo, 3 recomendações práticas (por exemplo: começar pelos que vencem primeiro, tratar à parte quem não tem consentimento).
- Se houver mais de 15 renovações, diga quantas ficaram de fora e ofereça continuar.

## Cuidados
- Não invente valores de prêmio, comissão ou probabilidade de renovação: só use o que as ferramentas retornaram.
- Não sugira texto de mensagem com dados que você não tem (telefone completo, CPF).
