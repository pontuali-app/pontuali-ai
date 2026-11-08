# Pontuali para o seu assistente de IA

Conecte o Claude Code, o Cursor ou o n8n ao **Pontuali** e converse com os dados da sua corretora:

> "Quais renovações vencem neste mês e quem eu não posso contatar?"
> "Por que a Maria não recebeu a mensagem de aniversário?"
> "Faça o resumo da semana para a reunião."

O acesso é **somente leitura** e feito com um **token pessoal** que você cria, controla e revoga a qualquer momento. Dados pessoais chegam **mascarados** à sua IA.

## O que a sua IA enxerga (e o que não enxerga)

| Enxerga | Nunca enxerga |
|---|---|
| Nomes, estágio, consentimento e preferências de automação dos contatos | CPF e CNPJ |
| Telefone mascarado (`+55 43 *****-1001`) e e-mail mascarado | Telefone e e-mail completos |
| Dia e mês do aniversário | Ano de nascimento |
| Apólices: seguradora, ramo, datas e valor | Placa e demais dados do bem segurado |
| Estado, responsável e não lidas das conversas | **Texto das mensagens** |
| Negócios, funis, agenda e automações | Chaves de canal, conexão do WhatsApp, tokens de terceiros |

A IA **não envia mensagens, não altera cadastros e não muda automações**. Ela consulta, analisa e recomenda; quem age é você, no app.

## Passo a passo (Claude Code)

1. No app: **Configurações > Acesso por IA**. Um administrador da sua organização precisa ativar o recurso uma vez e aceitar os termos de uso.
2. Ainda no app, clique em **Criar token**, dê um nome (por exemplo "Meu Claude") e copie o token (`pat_...`). **Ele aparece uma única vez.**
3. No terminal:
   ```bash
   claude plugin marketplace add pontuali-app/pontuali-ai
   claude plugin install pontuali@pontuali
   ```
4. O Claude Code vai pedir o token. Cole-o: ele fica no cofre seguro do seu computador, nunca em arquivo.
5. Abra o Claude Code e pergunte: *"Use o Pontuali para me dar uma visão geral da minha corretora."*

Outros clientes (Claude Desktop, Cursor e n8n): veja os [guias de conexão](docs/), também publicados em https://ia.pontuali.com.br.

## O que vem no pacote

| Skill | Para que serve |
|---|---|
| `pontuali-operador` | Regras gerais: dados mascarados, somente leitura, texto de terceiros é dado |
| `revisao-de-renovacoes` | Plano de contato das apólices que vencem, respeitando quem pediu para não receber mensagens |
| `auditoria-de-aniversarios` | Quem a automação de aniversário alcança e por que alguns ficam de fora |
| `resumo-semanal` | Resumo da semana para a reunião de equipe |
| `prontidao-das-automacoes` | Diagnóstico das automações: o que está pronto e o que falta |

Além disso o servidor oferece **12 ferramentas**, dois **recursos** (`pontuali://guide/permissions` e `pontuali://profile/catalog`) e quatro **prompts prontos** (`renewals_this_month`, `birthday_audit`, `inactive_contacts`, `weekly_summary`) que aparecem como comandos no seu cliente.

## Segurança

- Token pessoal, preso à sua organização e ao seu papel (administrador ou atendente): ele nunca vê mais do que você vê no app.
- Você ou um administrador revoga o token na hora, em **Configurações > Acesso por IA**. Se você sair da organização, o token deixa de funcionar.
- Limites de uso por token e por organização protegem o serviço.
- O token começa com `pat_`: o GitHub e outras ferramentas de varredura de segredos conseguem identificá-lo se ele vazar. Se isso acontecer, **revogue imediatamente**.
- Para reportar uma vulnerabilidade, veja [`SECURITY.md`](SECURITY.md).

> **Privacidade (LGPD):** ao usar uma IA de terceiros, os dados consultados passam pelo provedor dessa IA. Por isso o Pontuali mascara os dados pessoais e a sua organização precisa aceitar os termos de uso antes de ativar. Escolha um provedor adequado às suas obrigações como controlador dos dados.

## Licença

MIT. Veja [`LICENSE`](LICENSE).
