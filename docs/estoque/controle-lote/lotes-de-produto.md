# Tela Lotes de Produto

A tela **Lotes de Produto** é o ponto central de consulta e manutenção de lotes. Nela você pesquisa saldos, cadastra lotes manualmente, vê o histórico de cada lote e lança entradas ou saídas manuais com justificativa.

---

## Como acessar

**Produtos → Lotes de Produto**

![placeholder: menu Produtos com a opção Lotes de Produto destacada](img1.png)

---

## Permissões

| Permissão | Libera |
|-----------|--------|
| **Consultar produtos** (agrupador **Produtos**) | Abrir a tela |
| **Lançar movimentação manual de estoque** (agrupador **Estoque**) | Botões **Entrada manual** e **Saida manual** |

---

## Fluxo de uso

### 1. Pesquise na aba Pesquisa

| Filtro | Descrição |
|--------|-----------|
| **Produto** | Um ou mais produtos |
| **Fornecedor** | Um ou mais fornecedores. Útil quando o mesmo produto tem lotes de fornecedores diferentes |
| **Filial** | Mostra os lotes da filial escolhida. **(TODAS)** é a opção padrão. O combo some se você tem uma filial só |
| **Somente com saldo** | Oculta lotes sem saldo |
| **Tipo de Relatorio** | Muda a grade. Veja [Relatórios de Lote](relatorios.md) |
| Campo de pesquisa | Procura pelo número do lote ou pela descrição do produto |

A grade padrão mostra código, produto, lote, fabricação, validade, origem, fornecedor, código de agregação, saldo e filial.

![placeholder: aba Pesquisa com os filtros Produto, Fornecedor, Filial e Somente com saldo em destaque](img2.png)

### 2. Cadastre ou edite um lote na aba Cadastro

Use para lotes de abertura, ajustes ou cadastro antecipado.

| Campo | Descrição |
|-------|-----------|
| **Produto** | Produto do lote |
| **Fornecedor** | Opcional |
| **Numero do lote** | Obrigatório |
| **Fabricacao** | Data de fabricação. Pode ficar desmarcada |
| **Validade** | Só habilita se o produto controla validade. Pode ficar desmarcada |
| **Origem** | **C - Compra**, **P - Producao** ou **M - Manual**. Vem como **M - Manual** em lote novo |
| **Codigo de agregacao** | Uso em medicamentos. Deixe em branco nos demais produtos |

!!! info "Mesmo número em fornecedores diferentes"
    Compra pode repetir o número do lote entre fornecedores. Lote de **Producao** precisa ter número único para o produto, e o sistema bloqueia a repetição.

!!! warning "Lote com movimento não se exclui"
    Se o lote já tem movimentos, o sistema bloqueia a exclusão.

### 3. Consulte a aba Historico

Mostra os movimentos do lote selecionado.

| Coluna | Descrição |
|--------|-----------|
| **Data/Hora** | Quando ocorreu |
| **Tipo** | Entrada ou Saída |
| **Status** | Reserva ou Efetivado |
| **Quantidade** | Quantidade movimentada |
| **Filial** | Filial do movimento |
| **Origem** | NF Fornecedor, OP (lote), Consumo OP, NF Venda item ou Manual |
| **Observacao** | Texto do movimento. Obrigatório nos lançamentos manuais |

!!! info "Reserva e Efetivado"
    Ao salvar o item de uma nota de venda, o lote escolhido fica em **Reserva**. Ao faturar a nota, vira **Efetivado** e abate o saldo. Veja [Saída por Nota Fiscal de Venda](nf-venda.md).

![placeholder: aba Historico com a coluna Status mostrando uma linha Reserva e uma Efetivado](img3.png)

### 4. Lance entrada ou saída manual

Com lotes na grade, selecione o lote e clique em **Entrada manual** ou **Saida manual**. A janela mostra lote, produto e fornecedor e pede:

| Campo | Descrição |
|-------|-----------|
| **Filial** | Filial do movimento |
| **Quantidade** | Deve ser maior que zero |
| **Data** | Data do movimento |
| **Observacao (obrigatoria)** | Justifique o ajuste. Até 300 caracteres |

Clique em **Gravar**. O movimento também entra na movimentação manual de estoque do produto.

![placeholder: janela de movimento manual com o campo Observacao destacado](img4.png)

!!! warning "Data retroativa"
    Com data anterior a hoje, o sistema pergunta se você confirma. Se responder **Não**, usa a data de hoje.

!!! warning "Saída maior que o saldo"
    O sistema bloqueia saída maior que o saldo do lote na filial.

---

## Limitações da versão atual

- Os botões de movimento manual ficam ativos com qualquer linha na grade. O lote usado é o da linha selecionada.

<!--
??? note "Referência técnica"

    Fonte: fontes/uCadLoteProduto.pas / uCadLoteProduto.lfm (TfrmCadLoteProduto, herda TFormBaseCadastroCompleto)
    Menu: Produtos → Lotes de Produto (miLotesProdutoClick)
    Tabelas: LOTE_PRODUTO, LOTE_PRODUTO_MOV, VW_LOTE_PRODUTO_SALDO, MOV_MANUAL_PRODUTO
    Permissões: AbrirTela = 1 (msProdutos); movimento manual e lote de abertura = 5 (msProdutos)
    Movimento manual: grava MOV_MANUAL_PRODUTO e LancarMovimentoLote (status E); saldo conferido antes e dentro da transação
-->
