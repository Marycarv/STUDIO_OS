# STUDIO_OS — Central de Comando de Conteúdo com IA

**Status:** fase de estruturação e validação. Este repositório contém documentação e migrações propostas; ainda não representa um sistema implantado nem validado em produção.

## Princípios
- O banco de dados é a fonte de verdade.
- Cada vídeo tem um identificador permanente.
- Ativos sem evidência suficiente de direitos ficam pendentes ou bloqueados.
- Publicação externa exige aprovação humana explícita.
- Segredos e chaves de API nunca ficam no navegador, no repositório ou em prompts.
- IA auxilia a produção; não garante exatidão, direitos autorais ou monetização.

## Estrutura
- `00_MASTER/`: visão do projeto, arquitetura e decisões.
- `02_COMANDOS/`: catálogo de comandos.
- `03_BANCO_DE_DADOS/`: modelo, migrações e plano de testes.
- `04_PAINEL/`: mapa de telas.
- `05_AUTOMACOES/`: fluxos e gatilhos.
- `06_PRODUCAO/`: pipeline de vídeo.
- `07_DIREITOS_E_AUDITORIA/`: licenças e auditoria.
- `08_DISTRIBUICAO/`: publicação e reaproveitamento.
- `09_ANALYTICS/`: métricas e experimentos.
- `10_DOCUMENTACAO/`: decisões e próximos passos.

## Ordem de implementação
1. Revisar regras e modelo de dados.
2. Criar um projeto Supabase **de desenvolvimento**.
3. Aplicar as migrações em ordem e executar os testes de segurança.
4. Construir o painel MVP.
5. Integrar IA exclusivamente pelo backend seguro.
6. Adicionar automações com idempotência e logs.
7. Integrar publicação e métricas usando APIs oficiais quando aprovadas.

## Banco de dados
As migrações em `03_BANCO_DE_DADOS/` devem ser revisadas e testadas em um projeto Supabase isolado. **Não aplicar em produção antes de executar os testes documentados.** O primeiro usuário `owner` deve ser provisionado por backend confiável, não por autoatribuição no navegador.

## Situação atual
- Documentação inicial: em andamento.
- Migrações SQL: preparadas para revisão; ainda não executadas/validadas em banco real.
- Painel e integrações: ainda não implantados.
- Publicação automática: não habilitada; requer aprovação humana e controles de idempotência.
