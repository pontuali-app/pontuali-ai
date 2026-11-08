# Como contribuir

A branch `main` é protegida: **ninguém envia direto para ela** (nem administradores).

1. Crie uma branch e abra um Pull Request.
2. O check **`validate`** precisa passar: manifestos válidos, YAML das skills e nenhuma credencial `pat_` commitada. Outro check, **`pages`**, monta o site para pegar página quebrada antes do merge.
3. O PR precisa de **1 aprovação** de outra pessoa. Se você enviar um commit novo depois de aprovado, a aprovação cai e precisa ser refeita. As conversas do PR precisam estar resolvidas.
4. O merge é por **squash**. Depois do merge na `main`, o site é publicado sozinho em https://ia.pontuali.com.br.

## O que nunca entra aqui
- Tokens de acesso reais (`pat_...`), chaves ou senhas. O repositório é público.
- Dados de clientes, mesmo de exemplo.

Dúvidas sobre segurança: veja [`SECURITY.md`](SECURITY.md).
