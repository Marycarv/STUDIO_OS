# Banco de dados — modelo resumido

> Documento de orientação. Para implantar, consulte as migrações SQL completas e teste-as primeiro em um projeto Supabase de desenvolvimento. Este resumo não substitui os arquivos SQL.

## Entidades principais
- **workspaces**: isolamento organizacional.
- **workspace_members**: usuários, funções e estado de participação.
- **projects**: canais/projetos de conteúdo dentro do workspace.
- **ideas**: caixa de entrada e avaliação de pautas.
- **videos**: unidade principal de produção, código estável e status.
- **script_versions / script_sections**: versões imutáveis de roteiro e estrutura.
- **sources / claims**: fontes e afirmações a verificar.
- **assets**: arquivos, origem e evidências de direitos/licença.
- **approvals**: decisões humanas ligadas a alvos específicos.
- **audit/status history**: rastreabilidade de ações e transições.
- **tasks / automation runs**: execução, tentativas, resultados e erros.
- **publications / metrics**: distribuição e resultados por plataforma.

## Princípios de integridade
1. Cada registro operacional pertence a um workspace.
2. As permissões devem ser verificadas no servidor e reforçadas por RLS.
3. Aprovações referem-se a uma versão específica; alterar a versão invalida a aprovação anterior.
4. Direitos de assets incompletos ou bloqueados impedem a liberação final.
5. Transições de status devem passar por regras centralizadas.
6. Histórico de auditoria não deve ser editável como um campo comum.
7. Publicações precisam de idempotência para evitar duplicatas.
8. Segredos nunca são armazenados no navegador ou no repositório.
9. O primeiro proprietário do workspace deve ser provisionado por backend confiável, não por autoatribuição no cliente.
10. Testar isolamento entre dois usuários e dois workspaces antes de produção.

## Fluxo de vídeo
`idea → triage → research → fact_check → script_draft → script_review → storyboard → asset_rights → production → final_audit → ready_to_publish → scheduled/published → analysis`

## Antes de executar migrações
- Revisar SQL e compatibilidade com a versão do Supabase/PostgreSQL.
- Usar projeto de desenvolvimento e backup.
- Executar as migrações na ordem numerada.
- Rodar todos os testes do plano de testes.
- Verificar políticas RLS e funções SECURITY DEFINER.
- Não expor `service_role`.
- Não considerar o banco validado até executar os testes em ambiente real.

## Estado
Este resumo foi criado para orientar a leitura. A implantação continua pendente de aplicação e validação das migrações SQL completas.