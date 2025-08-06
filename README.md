## Fluxo Principal do Robô de Processamento de Pedidos de Empréstimo

1. **Leitura dos Dados do Excel**:
   - O robô começa abrindo um arquivo Excel chamado "PedidosEmprestimo.xlsx"
   - Lê os dados da planilha "Pedidos" e armazena em uma variável do tipo DataTable chamada `tabelaPedidosEmprestimo`

2. **Abertura do Sistema UiBank**:
   - Acessa o site do UiBank (https://uibank.uipath.com/loans/apply) usando o navegador Chrome

3. **Processamento de Cada Pedido**:
   - Para cada linha na tabela de pedidos (começando da linha 2), o robô executa as seguintes ações:
     a. Preenche o campo "Email Address of Requester" com o email do solicitante
     b. Preenche o campo "Loan Amount Requested" com o valor do empréstimo
     c. Seleciona o prazo do empréstimo (Loan Term) no dropdown
     d. Preenche o campo "Current Yearly Income" com a renda anual
     e. Preenche o campo "Age" com a idade do solicitante
     f. Clica no botão "Submit Loan Application"

4. **Verificação de Aprovação**:
   - Após enviar o pedido, verifica se a mensagem de aprovação aparece ("You've been approved for a loan with UiBank!")
     - Se aprovado: captura o ID do empréstimo e a taxa de juros (APR), registra no Excel como "APROVADO"
     - Se não aprovado: registra no Excel como "NÃO APROVADO!"

5. **Preparação para Próximo Pedido**:
   - Clica no botão "Apply For Another Loan" para voltar ao formulário inicial
   - Incrementa o contador para registrar na próxima linha do Excel

## Estrutura de Dados

- **Arquivo Excel de entrada**: Deve conter colunas com:
  - Email do solicitante
  - Valor do empréstimo
  - Prazo do empréstimo
  - Renda anual
  - Idade

- **Saída no Excel**: São adicionadas colunas com:
  - Status (APROVADO/NÃO APROVADO!)
  - ID do empréstimo (quando aprovado)
  - Taxa de juros (APR) (quando aprovado)

## Técnicas Utilizadas

1. **Seleção de Elementos UI**: Usa seletores robustos com fallback para Computer Vision quando necessário
2. **Tratamento de Exceções**: Verifica explicitamente se o pedido foi aprovado ou não
3. **Controle de Fluxo**: Usa loops para processar todos os pedidos da planilha
4. **Registro de Logs**: Grava informações de processamento para auditoria

Este robô é eficiente para processamento em massa de solicitações de empréstimo, reduzindo erros humanos e aumentando significativamente a produtividade no preenchimento de formulários.
