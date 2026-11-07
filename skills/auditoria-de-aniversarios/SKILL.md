---
name: auditoria-de-aniversarios
description: 'Audita a automação de aniversário: quem ela alcança e por que alguns contatos ficam de fora (sem data de nascimento, opt-out, pausa). Use quando o usuário perguntar sobre aniversariantes ou sobre por que alguém não recebeu a mensagem de aniversário.'
---

# Auditoria da automação de aniversário

Siga a skill `pontuali-operador`.

## Passo a passo
1. `list_automations` e localize `birthday_greeting`: está ligada? Qual a janela de envio e o modo de público?
2. `get_automation_audience` com `code` = `birthday_greeting`. Pagine até no máximo 3 páginas. Cada linha traz `whyNotCovered` quando a automação **não** vai rodar para aquele contato (por exemplo `contact.opted_out`).
3. Conte e agrupe os motivos. Os mais comuns: sem data de nascimento, opt-out, automações pausadas para o contato, contato desativado para esse tipo.
4. Para os aniversariantes dos próximos 7 dias use `list_upcoming_occasions` com `days` = 7 e itens de tipo `birthday`.

## Formato da resposta
- Resumo em uma frase: "X contatos cobertos, Y de fora".
- Tabela de motivos com a contagem de cada um.
- Aniversariantes dos próximos 7 dias (nome e dia/mês).
- A correção mais valiosa: normalmente "completar a data de nascimento de N contatos no app".

## Cuidados
- A data de nascimento vem só como dia e mês. Não tente descobrir a idade.
- Opt-out sempre prevalece: nunca recomende insistir com esses contatos.
