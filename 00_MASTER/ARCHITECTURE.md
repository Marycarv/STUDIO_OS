# Arquitetura proposta

## Componentes
- ChatGPT: interface conversacional.
- Painel web: operação e dashboard.
- Backend: autenticação, validação de comandos e regras.
- Supabase/PostgreSQL: fonte de verdade.
- Drive ou storage: arquivos pesados.
- n8n: automações.
- APIs externas: somente após validar permissões, custos e limites.

## Fluxo
1. Usuário envia comando.
2. Backend valida identidade, parâmetros, permissões e estado.
3. Ação é executada ou vira tarefa.
4. Resultado e logs são gravados.
5. Painel mostra o estado atualizado.
6. Ações críticas aguardam aprovação humana.

## Segurança
- Chaves secretas somente no backend.
- Autenticação e regras de acesso.
- Validação de entradas.
- Logs sem segredos.
- Proteção contra duplicação.
- Backups e plano de restauração.
- Confirmação antes de publicar, apagar ou gerar custos.