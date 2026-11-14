# Encerrar Nota Fiscal (Saída)

Ao encerrar uma nota fiscal de saída, você passa por uma janela em etapas antes de transmitir o documento à Sefaz. Na etapa de pagamento, o Factus sugere o plano e a forma de pagamento padrão do cliente.

---

## Como acessar

**Nota Fiscal/Faturamento → Nota Fiscal Vendas**, abra a nota e clique em **Encerrar** na barra de ferramentas.

![Tela de encerramento de nota fiscal com os campos Plano de Pagamento e Forma de Pagamento preenchidos automaticamente](img1.png)

---

## Permissões

| Permissão | Libera |
|-----------|--------|
| **Encerrar/Autorizar nota fiscal** (agrupador **Nota fiscal**) | Encerrar a nota |

---

## Fluxo de uso

### 1. Percorra as etapas

Na janela **Encerra nota fiscal.**, clique em **Proximo/Encerrar** para avançar. As etapas são:

1. **Observações**
2. **Volumes** (não aparece em nota de serviço)
3. **Outros valores**
4. **Descontos**
5. **Duplicatas**, com o **Plano Pagamento** e a **Forma pagamento acordado (opcional)**

A etapa **Duplicatas** só aparece se a licença inclui o módulo financeiro. Em nota de ajuste ou devolução, ela é pulada.

### 2. Confira a sugestão de pagamento

Se o cliente tem **Plano de Pagamento Padrão** e **Forma de Pagamento Padrão** na aba **Financeiro** do cadastro de parceiros, o Factus preenche os dois campos ao abrir a etapa.

| Situação | Comportamento |
|----------|---------------|
| Cliente tem padrão | Os campos vêm preenchidos |
| Cliente não tem padrão | Os campos ficam em branco. Você escolhe |
| A nota já tinha plano ou forma escolhidos | A sua escolha é mantida |

Você pode trocar os dois antes de continuar.

!!! info "Só plano principal"
    O plano padrão só é sugerido se for um plano principal, não uma parcela do plano.

### 3. Gere as parcelas e encerre

Clique em **Gerar** para montar as parcelas. O sistema exige:

- Plano de pagamento informado, em nota de saída.
- Parcelas geradas.
- Soma das parcelas igual ao valor total da nota.

Depois, clique em **Proximo/Encerrar** para concluir.

!!! warning "Não vale para nota gerada por pedido"
    Se a nota nasce de um pedido, a sugestão do cliente não é aplicada. Vale o plano do próprio pedido.

!!! warning "Nota com lote"
    Se a nota tem item que controla lote, a nota só encerra com a reserva de lote completa. Veja [Saída por Nota Fiscal de Venda](../../estoque/controle-lote/nf-venda.md).

---

## Limitações da versão atual

- A sugestão considera só o cadastro atual do cliente na nota.

**Prints faltando:**

- `img1.png`: etapa Duplicatas, com quadro vermelho nos campos **Plano Pagamento** e **Forma pagamento acordado (opcional)**.

<!--
??? note "Referência técnica"

    Fonte: fontes/uEncerraNotaFiscal.pas (MontarDuplicatas, FinalidadeSemFinanceiro) / uEncerraNotaFiscal.lfm; botão tbEncerrarDocumento em fontes/unotafiscal.pas
    Origem da sugestão: PESSOA.PES_PPGTO_CODIGO_PADRAO (só PPGTO_PAI nulo) e PES_FPG_CODIGO_PADRAO, aba Financeiro do parceiro
    Regra: só aplica se plano/forma ainda vazios e vTipoPedido = False
    Finalidade de emissão 3 e 4 pula Duplicatas (NT 2016.002, rejeição 871)
    Permissão: 13 (msNotaFiscal)
-->
