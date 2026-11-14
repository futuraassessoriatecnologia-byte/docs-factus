# Saída por Nota Fiscal de Venda

Ao vender um produto que controla lote, você escolhe de qual lote sai a mercadoria. O sistema sugere primeiro o lote que vence antes (FEFO) e não lista lotes vencidos.

---

## Como acessar

**Nota Fiscal/Faturamento → Nota Fiscal Vendas**, ao salvar um item de produto que controla lote.

![placeholder: tela Nota Fiscal Vendas com a aba de itens aberta](img1.png)

---

## Permissões

Valem as permissões de nota fiscal. Para faturar, **Encerrar/Autorizar nota fiscal** (agrupador **Nota fiscal**).

---

## Fluxo de uso

### 1. Salve o item na nota

Em nota de saída, depois que o item é salvo, abre a janela **Selecao de lote - saida em NF de venda (FEFO)**.

### 2. Escolha os lotes

A janela mostra produto, filial e a quantidade a distribuir. O grid lista os lotes com saldo disponível, do vencimento mais próximo ao mais distante:

| Coluna | Descrição |
|--------|-----------|
| **ID lote** / **Numero** | Identificação do lote |
| **Validade** | Vencimento |
| **Fornecedor** | Fornecedor do lote |
| **Saldo disp.** | Saldo livre, já descontadas as reservas de outras notas |
| **Qtd a usar** | Quantidade que sai desse lote. Você edita |

O botão **Auto FEFO** preenche as quantidades pelo vencimento. Ao abrir, ele já roda sozinho. Ajuste a quantidade, use outro lote ou divida entre vários. A linha **Restante / Distribuido / Falta** mostra a soma.

![placeholder: janela de seleção de lote FEFO com Auto FEFO e a coluna Qtd a usar destacados](img2.png)

!!! warning "Lotes vencidos não aparecem"
    Lotes vencidos ficam fora da lista. Se o saldo total não vencido não cobre a quantidade do item, o sistema avisa e não abre a janela. Ajuste a quantidade do item ou aguarde reposição.

!!! warning "A soma tem que fechar"
    A soma de **Qtd a usar** deve ser igual à quantidade do item. Quantidade acima do **Saldo disp.** também é bloqueada.

### 3. Confirme: a escolha vira reserva

Clique em **Confirmar**. A quantidade fica **reservada** no lote. O saldo disponível cai para novas vendas, mas o movimento ainda não é definitivo.

!!! info "Se a reserva falhar"
    Se outro usuário reservou o mesmo lote no meio tempo, o sistema avisa e reabre a janela. São até 3 tentativas.

### 4. Item sem reserva completa

Quando você fecha a janela com **Cancelar**, o sistema avisa que a nota não poderá ser faturada. O item sem reserva completa aparece em **salmão** no grid de itens. Clique com o botão direito no item e escolha **Reajustar lote (trocar sem mudar qty)** para reabrir a janela. A janela volta com as reservas atuais preenchidas.

![placeholder: grade de itens com linha em salmão e menu Reajustar lote aberto](img3.png)

### 5. Faturamento efetiva o movimento

Clique em **Encerrar**. Com a nota autorizada, as reservas viram movimentos **Efetivados** e o saldo do lote é abatido.

!!! warning "Faturamento bloqueado sem lote completo"
    Se algum item que controla lote não tem a reserva completa, o sistema lista os itens e bloqueia o faturamento.

!!! info "Falha ao efetivar depois de faturar"
    A nota autorizada na Sefaz não é desfeita. Se a efetivação falhar, o sistema avisa e registra no log. As reservas continuam como reserva.

### 6. Excluir ou cancelar libera o lote

Excluir o item libera a reserva. Cancelar ou inutilizar a nota na Sefaz estorna as reservas e os movimentos dos lotes.

---

## Limitações da versão atual

- O reajuste de lote só vale para nota de saída.

<!--
??? note "Referência técnica"

    Fonte: fontes/unotafiscal.pas (ProcessarReservaLoteItemNF, ValidarReservasLoteItens, EfetivarLotesItensNF, EstornarLotesItensNF, pmReajustarLoteClick, GridItensDrawColumnCell), fontes/uSelecaoLoteFEFO.pas
    Menu: Nota Fiscal/Faturamento → Nota Fiscal Vendas (miNotaFical); botão tbEncerrarDocumento 'Encerrar'
    Tabelas: LOTE_PRODUTO_MOV (INF_CODIGO, LOTM_STATUS R/E), VW_LOTE_PRODUTO_SALDO_DISPONIVEL
    Cor do destaque: $008080FF (SEM_LOTE = 'S')
    Permissão: 13 (msNotaFiscal) para encerrar
-->
