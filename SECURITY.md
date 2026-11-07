# Política de segurança

## Reportar uma vulnerabilidade

Envie os detalhes por e-mail para **seguranca@pontuali.com.br** (ou abra um relato privado em *Security > Report a vulnerability* neste repositório). Não abra uma issue pública com detalhes de exploração.

Inclua, se possível: o que você encontrou, como reproduzir, o impacto que enxerga e a versão do plugin. Respondemos em até **3 dias úteis** e mantemos você informado até a correção.

## O que está no escopo

- Este plugin (manifestos, skills, prompts e guias).
- O servidor MCP `https://mcp.pontuali.com.br/mcp` e o fluxo de tokens de acesso.

## Boas práticas para quem usa

- O token (`pat_...`) é uma senha: não o cole em chats, e-mails, issues ou arquivos versionados.
- Se o token vazar, revogue-o em **Configurações > Acesso por IA** no app.
- Prefira um token por ferramenta ou pessoa, com validade curta.

## Varredura de segredos

Tokens de acesso do Pontuali têm o formato `pat_` seguido de 43 caracteres base64url (`pat_[A-Za-z0-9_-]{43}`). Use essa expressão em ferramentas de varredura (por exemplo, um padrão personalizado do GitHub Secret Scanning ou do gitleaks).
