# Guias de conexão

Antes de qualquer cliente, você precisa de um **token**: no app, **Configurações > Acesso por IA** (um administrador ativa o recurso uma vez), depois **Criar token**. Copie o valor que começa com `pat_`: ele só aparece uma vez.

Endereço do servidor (igual para todos): `https://mcp.pontuali.com.br/mcp`
Autenticação: cabeçalho `Authorization: Bearer pat_...`

## Situação de cada cliente

| Cliente | Como conectar | Situação |
|---|---|---|
| Qualquer cliente MCP compatível | Endereço acima + cabeçalho `Authorization` | **Verificado pela Pontuali** com o cliente oficial do SDK MCP (`initialize`, `tools/list`, `tools/call`, recursos e prompts), contra o servidor real em Docker |
| Claude Code | Plugin (recomendado) ou `claude mcp add` | Configuração conforme a documentação oficial; **ainda não testada ponta a ponta pela Pontuali** |
| Cursor | `~/.cursor/mcp.json` | Idem |
| Claude Desktop | Via `mcp-remote` | Idem |
| n8n | Nó "MCP Client Tool" | Idem |
| claude.ai (web) e ChatGPT (conectores) | Exigem OAuth | **Ainda não suportado**: previsto para um próximo ciclo |

Se algo não funcionar no seu cliente, veja "Problemas comuns" abaixo e nos conte.

## Claude Code

Com o plugin (traz as skills e pede o token no cofre seguro):
```bash
claude plugin marketplace add pontuali-app/pontuali-ai
claude plugin install pontuali@pontuali
```
Sem o plugin (só o servidor):
```bash
export PONTUALI_TOKEN=pat_...
claude mcp add --transport http pontuali https://mcp.pontuali.com.br/mcp --header "Authorization: Bearer $PONTUALI_TOKEN"
```

## Cursor

Em `~/.cursor/mcp.json` (ou `.cursor/mcp.json` do projeto):
```json
{
  "mcpServers": {
    "pontuali": {
      "url": "https://mcp.pontuali.com.br/mcp",
      "headers": { "Authorization": "Bearer ${env:PONTUALI_TOKEN}" }
    }
  }
}
```
Defina `PONTUALI_TOKEN` no ambiente em vez de escrever o token no arquivo.

## Claude Desktop

O Claude Desktop lê servidores locais por arquivo; para um servidor remoto use o proxy `mcp-remote`. Em `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "pontuali": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://mcp.pontuali.com.br/mcp", "--header", "Authorization:${PONTUALI_AUTH}"],
      "env": { "PONTUALI_AUTH": "Bearer pat_..." }
    }
  }
}
```
Atenção: aqui o token fica no arquivo de configuração. Proteja o arquivo e prefira um token com validade curta.

## n8n

Adicione o nó **MCP Client Tool** ao seu fluxo de agente de IA: transporte *HTTP Streamable*, URL `https://mcp.pontuali.com.br/mcp`, autenticação por cabeçalho com `Authorization: Bearer pat_...` (guarde o token em uma credencial do n8n).

## Problemas comuns

| Sintoma | Causa provável | O que fazer |
|---|---|---|
| `401` / "not valid" | Token errado, expirado, revogado, ou o acesso por IA foi desativado na organização | Crie um novo token; peça a um administrador para conferir o acesso por IA |
| `429` / "too many requests" | Limite de uso por token ou organização | Espere o tempo indicado em `Retry-After` e reduza a frequência; não repita em laço |
| Resposta "Not found" para um contato | O identificador não é da sua organização ou não existe | Busque de novo com `search_contacts` |
| A IA diz que não pode enviar mensagens | É esperado: o acesso é somente leitura | Faça o envio no app |
