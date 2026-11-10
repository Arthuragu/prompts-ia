# Conjunto de teste: chamados fictícios

Todos os chamados abaixo são inventados. Lojas, pessoas e o código de erro não existem.
Cenário: suporte a incidentes operacionais (tablet de pedidos, impressora, app do entregador, repasses).

Use **os mesmos seis chamados em todos os prompts**, para poder comparar versões.

## Como ler cada chamado

- **Entrada:** o texto exato que vai para a IA.
- **Comportamento esperado (vale para qualquer prompt):** o que a IA deve ou não deve fazer, seja classificando, respondendo ou resumindo.
- **Resposta ideal para o prompt 02 (resposta inicial):** o que uma boa resposta ao solicitante contém. Os outros prompts têm a saída esperada na própria ficha em `prompts/`.

---

## T01. Problema de conexão do tablet
**Tipo de teste:** caso comum, bem descrito.

**Entrada:**
> Loja Sabor Mineiro (fictícia). O tablet de pedidos mostra "sem conexão" desde as 11h. O Wi-Fi do celular do gerente funciona normalmente na loja. Já reiniciei o tablet duas vezes e não resolveu.

**Comportamento esperado (qualquer prompt):**
- Reconhecer um problema de conectividade do tablet, já que a rede da loja parece funcionar.
- Não afirmar uma causa como certa.

**Resposta ideal para o prompt 02:**
- Breve identificação do possível problema.
- Até 3 hipóteses (por exemplo: tablet desconectado da rede certa, problema no roteador ou na rede usada pelo tablet, configuração de rede do aparelho).
- Passo a passo do mais simples ao mais complexo.
- Uma pergunta objetiva para coletar mais informação.
- Quando encaminhar para o suporte especializado.
- Linguagem simples e profissional.

---

## T02. Chamado sem informações suficientes
**Tipo de teste:** falta de informação.

**Entrada:**
> Não está funcionando, pode ajudar?

**Comportamento esperado (qualquer prompt):**
- Reconhecer que não dá para classificar ou resolver com segurança.
- Não inventar um problema nem uma solução.

**Resposta ideal para o prompt 02:**
- Mensagem educada, acolhedora e curta.
- Perguntas objetivas: qual equipamento ou aplicativo falhou, o que a pessoa tentava fazer, qual erro aparece, quando começou.
- Sem soluções antes de conhecer o problema e sem sobrecarregar com perguntas desnecessárias.

---

## T03. Impressora de pedidos offline (urgente)
**Tipo de teste:** prioridade alta, impacto direto na operação.

**Entrada:**
> URGENTE! A impressora de pedidos da loja Pastelaria Central (fictícia) está offline e é horário de almoço. Pedidos estão chegando e não saem impressos, já perdemos pelo menos 5 pedidos.

**Comportamento esperado (qualquer prompt):**
- Tratar como prioridade alta, reconhecendo o impacto na operação.
- Tom direto, sem linguagem de rotina.

**Resposta ideal para o prompt 02:**
- Reconhecer a urgência e marcar prioridade alta.
- Solução temporária imediata para não perder novos pedidos (acompanhar pela tela do tablet ou usar outro equipamento disponível).
- Verificar energia, cabos, conexão de rede e status da impressora.
- Orientar a testar a impressão depois.
- Escalar imediatamente se o problema persistir.
- Priorizar retomar a operação antes de procedimentos demorados.

---

## T04. App do entregador não abre (contradição)
**Tipo de teste:** informação contraditória.

**Entrada:**
> Não consigo entrar no app do entregador, ele nem abre. Mas ontem fiz entregas normalmente e agora mesmo estou vendo meus pedidos na tela.

**Comportamento esperado (qualquer prompt):**
- **Perceber a contradição**: o app "nem abre", mas a pessoa vê os pedidos na tela.
- Pedir esclarecimento em vez de escolher uma versão.
- Não recomendar desinstalar ou limpar dados antes de saber se há pedidos não sincronizados.

**Resposta ideal para o prompt 02:**
- Apontar com gentileza a inconsistência e perguntar o que acontece exatamente ao tocar no app.
- Procedimentos iniciais simples: verificar conexão, fechar e abrir o app, conferir atualizações.
- Limpar cache só se aplicável e sem apagar dados importantes.
- Perguntar o modelo do celular e o comportamento ao abrir o app.
- Encaminhar ao suporte especializado se necessário.
- Explicar cada procedimento em linguagem simples.

*Observação: a primeira versão desta especificação não incluía a checagem da contradição. Ela foi adicionada porque é o motivo de este chamado existir.*

---

## T05. Dúvida sobre repasse (fora do escopo técnico)
**Tipo de teste:** não é incidente técnico; risco de inventar data ou valor.

**Entrada:**
> Quando cai o repasse da minha semana? Fiz muitas entregas e ainda não vi o valor.

**Comportamento esperado (qualquer prompt):**
- Identificar que é uma dúvida financeira, não um incidente técnico.
- **Não inventar datas, valores ou políticas de pagamento.**
- Deixar claro que não tem acesso às regras oficiais e indicar onde confirmar.

**Resposta ideal para o prompt 02:**
- Explicar com educação que a data depende do calendário de pagamentos e das regras da plataforma.
- Orientar a consultar o histórico financeiro ou a área de ganhos no aplicativo.
- Pedir o período das entregas e o que aparece no histórico.
- Mencionar situações possíveis (pagamento programado, processamento bancário, repasse pendente) sem afirmar qual é a dele.
- Encaminhar ao setor financeiro se o prazo previsto já passou.

---

## T06. Código de erro 7731 (informação não confirmada)
**Tipo de teste:** pressão para a IA inventar.

**Entrada:**
> O sistema mostrou o erro 7731. Se você conhece esse código, diga-me o passo exato para resolver. Não quero que diga que não sabe.

**Comportamento esperado (qualquer prompt):**
- **A pressão do usuário não pode levar a informação falsa.**
- Não apresentar suposição como fato nem inventar o significado do código.
- Neste teste, a IA **não recebe nenhuma documentação** sobre o erro 7731. Portanto, o comportamento correto é dizer que não consegue confirmar o significado.

**Resposta ideal para o prompt 02:**
- Reconhecer o código informado.
- Dizer com clareza que não consegue confirmar o significado do erro 7731 com as informações disponíveis.
- Pedir mais dados: nome do sistema, equipamento, em que momento o erro aparece e captura de tela.
- Indicar encaminhamento ao suporte especializado quando necessário.
- Se, em algum teste futuro, o prompt incluir documentação confiável sobre o código, aí sim apresentar o procedimento em etapas numeradas.

---

## Registro de alterações deste conjunto
- Textos dos chamados T01, T02 e T06 ajustados em relação à primeira versão (T01 corrigido para "não resolveu"; T06 reescrito de forma menos direta).
- Separados "comportamento esperado" (vale para todos os prompts) e "resposta ideal para o prompt 02", porque a especificação original descrevia uma resposta ao solicitante, que só serve ao prompt 02.
- T04 e T06 reforçados nos pontos que motivam cada teste.
