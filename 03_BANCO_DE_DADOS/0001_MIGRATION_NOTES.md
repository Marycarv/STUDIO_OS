# STUDIO_OS — Migração 0001: notas de implementação

**Estado:** arquivo inicial para revisão e testes; ainda não executado em banco real.

## Conteúdo previsto
- 19 tabelas operacionais, constraints, índices e gatilhos `updated_at`.
- Funções auxiliares de membership/roles e RLS habilitada nas tabelas.
- Isolamento por `workspace_id` para os dados operacionais.
- Índices para filtros frequentes do painel e chaves de idempotência.

## Antes de aplicar
1. Crie um projeto Supabase de desenvolvimento e faça backup se já houver dados.
2. Execute em ambiente de teste, não em produção.
3. Valide a sintaxe com a ferramenta de migrações do Supabase/CLI.
4. Teste o onboarding de workspace: a criação do primeiro `owner` deve ocorrer por backend confiável em transação; o navegador não pode promover a si mesmo.
5. Teste RLS com dois usuários e dois workspaces diferentes.
6. Implemente e valide as regras de transição de status, aprovação humana, direitos de ativos, publicação e imutabilidade de roteiro/logs antes de tratar o sistema como seguro para produção.

## Limitações conhecidas da primeira migração
- As regras de publicação são documentadas, mas não implementadas como um gate transacional completo nesta migração.
- A validação de `approvals.target_id` é polimórfica e precisa de função/backend confiável.
- RLS de escrita usa uma política inicial por papel; operações críticas precisam de restrições adicionais antes de produção.
- Não há tabela para tokens de integração. Credenciais devem ficar em secret manager/integrações protegidas, nunca em tabelas de conteúdo.
- Relacionamentos opcionais compostos usam `RESTRICT` em vez de `SET NULL`, pois zerar a FK composta também tentaria zerar `workspace_id`, que é obrigatório. Arquive registros em vez de apagar entidades com histórico.
