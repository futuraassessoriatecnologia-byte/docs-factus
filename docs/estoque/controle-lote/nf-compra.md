# Entrada por Nota Fiscal de Compra

Ao receber um produto que controla lote, o Factus precisa saber de qual lote veio cada quantidade. Isso acontece ao encerrar a nota de fornecedor com **Movimentar Estoque** marcado.

---

## Como acessar

**Entradas → NF Fornecedor**, abra a nota e clique para encerrar. Abre a janela **Encerrar nota fiscal fornecedor**, aba **Encerramento**.

![placeholder: janela de encerramento da NF fornecedor com Movimentar Estoque destacado](img1.png)

---

## Fluxo de uso

### 1. Lote vindo do XML

Se você importou o XML e ele traz os dados de rastreabilidade (lote, quantidade, fabricação, validade), o Factus cria o lote e o vincula ao item sozinho.

!!! info "XML parcial ou a mais"
    Se o XML cobre só parte da quantidade, o sistema abre a janela de lotes ao encerrar. Ela já mostra o que veio do XML. Ajuste, remova ou adicione linhas até a soma bater.

### 2. Encerre a nota

Marque **Movimentar Estoque** e clique em **Proximo/Encerrar**. Para cada item de produto que controla lote e ainda não tem a quantidade toda distribuída, abre a janela **Captura de lote - encerramento de NF fornecedor**.

### 3. Distribua a quantidade em lotes

A janela mostra fornecedor, produto e a linha **Qtd alvo / Distribuido / Falta**. Preencha o grid:

| Coluna | Descrição |
|--------|-----------|
| **Numero do lote** | Identificação do lote |
| **Quantidade** | Quantidade desse lote |
| **Fabricacao (dd/mm/aaaa)** | Data de fabricação |
| **Validade (dd/mm/aaaa)** | Obrigatória se o produto controla validade |
| **Cod. agregacao** | Opcional, uso em medicamentos |

Use **Adicionar lote** e **Remover lote** para ajustar as linhas. Com um único lote, a primeira linha já vem com a quantidade total.

!!! info "Quantidade em unidades de estoque"
    A quantidade alvo considera a embalagem. Dez caixas com 6 unidades cada pedem 60.

![placeholder: janela de captura de lote com a linha Qtd alvo / Distribuido / Falta destacada](img2.png)

!!! warning "A soma tem que fechar"
    Com quantidade a menos, o sistema avisa "Faltam N unidades a distribuir em lotes". Com a mais, avisa "Sobram N unidades". A janela reabre com o que você digitou.

!!! warning "Validade vencida"
    Se o produto controla validade, a data deve ser posterior a hoje. Lote de compra não nasce vencido.

### 4. Confirme

Clique em **Confirmar**. Os lotes são criados (ou reaproveitados, se o fornecedor já tem o mesmo número) e a entrada é registrada.

!!! warning "Cancelar desfaz o encerramento"
    Se você clicar em **Cancelar** na janela de lotes, o encerramento da nota inteira é desfeito. Nada fica gravado pela metade.

---

## XML com lote para produto sem controle

Se o XML traz lote para um produto que não controla lote, o Factus descarta os dados, avisa na tela quais produtos são e registra o fato no log. Veja se o produto deveria controlar lote em [Habilitando o controle de lote](habilitando.md).

---

## Excluir item de nota com lote

Ao excluir um item da NF Fornecedor, o sistema desfaz os lotes que ele gerou. Se esses lotes já tiveram saída ou reserva em venda ou produção, o sistema bloqueia a exclusão. Cancele antes as saídas e as reservas.

---

## Limitações da versão atual

- Não existe rotina para cancelar uma NF Fornecedor já encerrada. Peça orientação ao suporte antes de qualquer cancelamento.

<!--
??? note "Referência técnica"

    Fonte: fontes/uEncerrarNFFornecedor.pas (CapturarLotesItensSemRastro), fontes/uCadLoteProduto.pas (AbrirModoNFFornecedor), fontes/uNotaFiscalFornecedor.pas (importação XML, ExecutaExcluirExtra)
    Menu: Entradas → NF Fornecedor (miNotaFiscalEntrada)
    Tabelas: LOTE_PRODUTO, LOTE_PRODUTO_MOV (INFF_CODIGO), ITENS_NOTA_FISCAL_FORNECEDOR
    Qtd alvo = INFF_QUANTIDADE * COALESCE(INFF_QTD_EMBALAGEM,1); tolerância 0,0005
    Log do XML descartado: ação IMPORT_XML_RASTRO_IGNORADO
-->
