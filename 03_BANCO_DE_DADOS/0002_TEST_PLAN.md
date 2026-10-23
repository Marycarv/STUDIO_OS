# STUDIO_OS — plano de testes da migração 0002

**Status:** testes planejados; ainda não executados em um Supabase real.

## Antes de executar
1. Criar um projeto Supabase de desenvolvimento separado da produção.
2. Aplicar `0001_initial_schema.sql` e confirmar que termina sem erros.
3. Aplicar `0002_business_rules.sql` e confirmar que termina sem erros.
4. Criar dois usuários de teste e dois workspaces independentes.
5. Executar testes com sessão autenticada de cada usuário; não testar tudo com `service_role`, pois ela ignora RLS.

## Casos obrigatórios

| ID | Cenário | Resultado esperado |
|---|---|---|
| DB-001 | Usuário A consulta registros do workspace B sem ser membro | Nenhuma linha retornada; escrita negada |
| DB-002 | Cliente tenta alterar `videos.status` diretamente | Negado por ausência de política de UPDATE |
| DB-003 | Cliente tenta alterar ou apagar conteúdo de uma versão de roteiro existente | Trigger rejeita a operação |
| DB-004 | Cliente tenta inserir roteiro já com status `approved` | Trigger rejeita a inserção |
| DB-005 | Cliente tenta inserir aprovação já aprovada | Trigger rejeita a inserção; novo pedido começa `pending` |
| DB-006 | Editor tenta gravar diretamente uma revisão de direitos | Negado; usar `record_asset_rights_check` |
| DB-007 | Revisão de direitos `cleared` sem permissão comercial ou sem evidência | RPC rejeita a operação |
| DB-008 | Ativo obrigatório sem revisão `cleared` válida | Gate de direitos retorna `false` |
| DB-009 | Ativo com direitos expirados | Gate de direitos retorna `false` |
| DB-010 | Vídeo sem versão de roteiro aprovada atual | Gate final retorna `false` |
| DB-011 | Alegação crítica/alta não verificada ou contradita | Gate final retorna `false` |
| DB-012 | Vídeo sem aprovação `final_quality` | Gate final retorna `false` |
| DB-013 | Transição de status fora do fluxo permitido | RPC lança erro e não altera o vídeo |
| DB-014 | Transição válida de status | Vídeo, histórico e auditoria são gravados na mesma transação |
| DB-015 | Transição para `scheduled` sem aprovação humana `publish` | RPC rejeita a operação |
| DB-016 | Tentativa de marcar vídeo como `published` via RPC genérica | RPC rejeita; apenas fluxo confiável de publicação poderá marcar publicado |
| DB-017 | Tentativa de atualizar/apagar `audit_logs` ou `video_status_history` | Trigger rejeita a operação |
| DB-018 | Repetir chamada de automação com mesma chave de idempotência | Validar unicidade; chamadas não devem duplicar efeitos externos |

## Limitações que ainda exigem implementação
- O primeiro `owner` do workspace deve ser criado atomicamente por backend confiável; não liberar autoatribuição ao navegador.
- A migração não implementa ainda uma RPC de publicação nem um bloqueio transacional completo contra duplicação de efeitos externos. A API de publicação deve usar chave de idempotência e confirmar a plataforma antes de marcar como publicado.
- `service_role` ignora RLS; nunca pode ser enviada ao navegador, ao prompt da IA ou a um workflow com permissões excessivas.
- Revisar permissões das funções `SECURITY DEFINER`, grants e isolamento antes de produção.
- Executar testes de carga quando houver volume real; os índices iniciais são uma base, não uma otimização final.

## Critério de conclusão
A migração só pode ser considerada validada depois que DB-001 a DB-017 forem executados e aprovados em ambiente de desenvolvimento. DB-018 depende da implementação do executor de automação.
