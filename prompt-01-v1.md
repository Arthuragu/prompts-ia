# Prompt 01, v1: saída bruta

Saída recebida dos 6 chamados. Os campos `id` e a lista `chamados` mostram que os 6 foram processados juntos, numa mesma conversa.

```json
{
  "chamados": [
    {"id": "T01", "categoria": "Problema de conexão / Rede Wi-Fi", "prioridade": "média",
     "justificativa": "O tablet de pedidos está sem conexão, prejudicando a operação da loja. Como o Wi-Fi funciona em outros dispositivos e as reinicializações não resolveram, é necessário investigar uma possível falha de configuração ou conexão do tablet."},
    {"id": "T02", "categoria": "Solicitação de suporte / Problema não identificado", "prioridade": "baixa",
     "justificativa": "O chamado não apresenta informações suficientes para identificar o problema. É necessário solicitar detalhes sobre o equipamento, sistema, erro apresentado e momento em que a falha ocorre."},
    {"id": "T03", "categoria": "Impressora / Falha de comunicação", "prioridade": "alta",
     "justificativa": "A impressora está offline durante o horário de almoço, impedindo a impressão dos pedidos e causando prejuízo operacional. Já existem pelo menos cinco pedidos afetados, exigindo atendimento imediato."},
    {"id": "T04", "categoria": "Aplicativo / Falha de inicialização", "prioridade": "média",
     "justificativa": "O aplicativo do entregador não abre, impedindo o acesso normal às suas funcionalidades. Entretanto, os pedidos continuam visíveis na tela, indicando que pode existir uma falha específica no aplicativo, sem evidência de interrupção total da operação."},
    {"id": "T05", "categoria": "Financeiro / Repasse de pagamentos", "prioridade": "baixa",
     "justificativa": "O entregador solicita informações sobre o pagamento semanal, mas não apresenta evidências de atraso ou falha financeira. É necessário consultar o calendário de repasses e o histórico de pagamentos."},
    {"id": "T06", "categoria": "Sistema / Código de erro", "prioridade": "média",
     "justificativa": "O código 7731 indica uma ocorrência que precisa ser investigada, mas não há informações sobre o sistema ou contexto da falha. É necessário identificar a origem do erro antes de fornecer instruções de correção, evitando soluções inventadas ou procedimentos inadequados."}
  ]
}
```
