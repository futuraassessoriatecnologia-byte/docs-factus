# Rastreabilidade no XML da NF-e

Para produtos que controlam lote, o XML da NF-e de venda informa os lotes de onde a mercadoria saiu. Isso atende exigências de rastreabilidade e ajuda na conferência por contador e auditor.

---

## Como acessar

Não há tela própria. O grupo de rastreabilidade entra no XML quando você emite a nota em **Nota Fiscal/Faturamento → Nota Fiscal Vendas**.

![placeholder: tela Nota Fiscal Vendas com o botão Encerrar destacado](img1.png)

---

## O que muda no XML

Cada item de produto que controla lote ganha um bloco de rastreabilidade por lote vendido, com número do lote, quantidade, data de fabricação, validade e código de agregação (quando houver). Item dividido entre dois lotes gera dois blocos.

| Situação | O que acontece |
|----------|----------------|
| Produto não controla lote | O XML sai como antes, sem bloco |
| Lote sem data de validade | O bloco desse lote **não** é emitido |
| Lote sem número | O bloco não é emitido |
| Movimento ainda em reserva | Não entra. Só entram lotes efetivados |

!!! warning "Lote sem validade fica fora do XML"
    Produto que controla só lote, sem validade, não gera o bloco de rastreabilidade. Se o seu cliente exige o bloco, cadastre a validade nos lotes.

---

## Geração é automática

Você não preenche nada para o XML. Os dados vêm da reserva feita ao salvar o item na nota, conforme [Saída por Nota Fiscal de Venda](nf-venda.md).

!!! tip "Conferência"
    Para conferir o que foi emitido, abra a aba **Historico** em [Lotes de Produto](lotes-de-produto.md). O movimento efetivado da nota mostra o mesmo lote e a mesma quantidade do XML.

<!--
??? note "Referência técnica"

    Fonte: fontes/DFe/uDocumentoDFe.pas (Grupo I80, tag <rastro>: nLote, qLote, dFab, dVal, cAgreg)
    Origem: LOTE_PRODUTO_MOV com INF_CODIGO do item e LOTM_STATUS = 'E', LOTM_QUANTIDADE > 0,0005
    Regra: lote sem LOT_VALIDADE não emite <rastro>; ordem por validade (nulos por último) e LOTM_CODIGO
-->
