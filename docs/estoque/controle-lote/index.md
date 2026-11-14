# Controle de Lote e Validade

O Controle de Lote e Validade rastreia cada produto do recebimento até a venda. Cada unidade que entra, sai ou é consumida fica ligada a um lote de origem, com fornecedor, data de fabricação e, quando o produto vence, a validade.

O controle é **opcional por produto**: só atua nos produtos em que você marcar essa opção. Os demais continuam funcionando como antes.

---

## Como acessar

A tela de consulta fica em **Produtos → Lotes de Produto**. As demais etapas aparecem dentro das telas que você já usa (produto, NF Fornecedor, Nota Fiscal Vendas e Ordem de Produção).

![placeholder: menu Produtos com a opção Lotes de Produto destacada](img1.png)

---

## O que muda no dia a dia

| Área | O que muda |
|------|-----------|
| Cadastro de produto | Duas opções novas: **Controla lote** e **Controla validade** |
| Compra (NF Fornecedor) | Ao encerrar a nota, você informa o lote de cada item, ou o sistema lê o lote do XML |
| Venda (Nota Fiscal Vendas) | Ao salvar o item, você escolhe de qual lote sai a mercadoria. O sistema sugere o que vence primeiro |
| Produção (Ordem de Produção) | Ficam registrados o lote da matéria-prima consumida e o lote do produto acabado |
| Consulta | Tela **Lotes de Produto** com saldo, histórico e lançamento manual de entrada e saída |
| Relatórios | Lotes a vencer, lotes sem movimento e auditoria de saldo |
| NF-e | O XML da venda leva os lotes de cada item |

---

## Páginas desta seção

1. [Habilitando o controle de lote num produto](habilitando.md)
2. [Tela Lotes de Produto](lotes-de-produto.md)
3. [Relatórios de Lote](relatorios.md)
4. [Entrada por Nota Fiscal de Compra](nf-compra.md)
5. [Saída por Nota Fiscal de Venda](nf-venda.md)
6. [Consumo e produção em Ordem de Produção](ordem-producao.md)
7. [Rastreabilidade no XML da NF-e](xml-nfe-rastro.md)

!!! tip "Por onde começar"
    Comece por [Habilitando o controle de lote num produto](habilitando.md). Sem essa etapa, nenhuma tela de compra, venda ou produção pede lote.

---

## Permissões

| Permissão | Libera |
|-----------|--------|
| **Consultar produtos** (agrupador **Produtos**) | Abrir a tela **Lotes de Produto** |
| **Lançar movimentação manual de estoque** (agrupador **Estoque**) | Entrada manual, saída manual e lote de abertura |

As permissões ficam no cadastro de usuários. As demais telas seguem as permissões que elas já tinham.

---

## Limitações da versão atual

- O saldo do lote é controlado por filial, mas o **saldo geral do produto** (usado na auditoria) não separa filiais.
- Não existe rotina para reabrir uma Ordem de Produção encerrada nem para cancelar uma NF Fornecedor já encerrada. Nos dois casos, peça apoio ao suporte.

<!--
??? note "Referência técnica"

    Fontes: fontes/uCadLoteProduto.pas, uLoteProdutoFuncoes.pas, uSelecaoLoteFEFO.pas, uLoteValidade.pas, PCP/uEncerramentoLoteOP.pas
    Menu: Produtos → Lotes de Produto (miLotesProdutoClick em uPrincipal.pas)
    Tabelas: LOTE_PRODUTO, LOTE_PRODUTO_MOV, VW_LOTE_PRODUTO_SALDO, VW_LOTE_PRODUTO_SALDO_DISPONIVEL; flags PRO_CONTROLA_LOTE / PRO_CONTROLA_VALIDADE em PRODUTO
    Permissões (MENUS): 1 = Consultar produtos (msProdutos) abre a tela; 5 = Lançar movimentação manual de estoque (msProdutos) para movimento manual e lote de abertura
    Scripts SQL: 608-610, 629-639
-->
