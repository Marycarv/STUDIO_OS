# Catálogo de automações

## Nova pauta
Gatilho: pauta criada. Ações: gerar ID, registrar triagem. Evitar duplicação.

## Pesquisa aprovada
Gatilho: aprovação da pesquisa. Ações: criar tarefa de roteiro. Bloquear se fontes forem insuficientes.

## Roteiro aprovado
Gatilho: aprovação de versão. Ações: criar tarefa de storyboard. Nova edição invalida aprovação antiga.

## Auditoria de direitos
Gatilho: auditoria solicitada ou asset alterado. Ações: validar campos e evidências. Não presumir licença.

## Publicação
Gatilho: solicitação explícita. Validar checklist, permissões e aprovação final.

Cada execução registra ID, gatilho, entrada, horário, resultado, erro e tentativas.