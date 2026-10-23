# Catálogo de comandos

Estes comandos são especificações; só serão executáveis depois da implementação.

| Comando | Ação | Aprovação |
|---|---|---|
| `STATUS` | Consulta vídeos, tarefas e pendências | Não |
| `NOVA PAUTA` | Cria pauta com ID | Não |
| `PESQUISAR NICHO` | Cria tarefa de pesquisa | Não |
| `PESQUISAR PAUTA VID-001` | Registra fontes e pesquisa | Revisão factual |
| `CRIAR ROTEIRO VID-001` | Gera versão de roteiro | Sim |
| `AUDITAR DIREITOS VID-001` | Analisa assets e pendências | Revisão humana |
| `APROVAR ROTEIRO VID-001` | Aprova versão específica | Sim |
| `PREPARAR PUBLICAÇÃO VID-001` | Prepara metadados e checklist | Sim |
| `PUBLICAR VID-001` | Solicita publicação se integração existir | Sempre |
| `RELATÓRIO SEMANAL` | Resume operação e métricas | Não |

Formato de retorno: `command_id`, `status`, `summary`, `artifacts`, `warnings`, `next_actions`, `created_at`.