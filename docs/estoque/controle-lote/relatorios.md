# Relatórios de Lote

Os relatórios de lote são quatro modos de visualização da tela **Lotes de Produto**: todos com saldo, lotes a vencer, lotes sem movimento e auditoria de saldo. O sistema também avisa, ao abrir, quando há lotes vencidos com saldo.

---

## Como acessar

**Produtos → Lotes de Produto**, aba **Pesquisa**. Escolha o **Tipo de Relatorio** no combo. A grade recarrega. Para gerar o PDF, clique em **Imprimir** na barra de ferramentas.

![placeholder: combo Tipo de Relatorio aberto com os quatro tipos](img1.png)

---

## Permissões

Vale a permissão **Consultar produtos** (agrupador **Produtos**), a mesma da tela.

---

## Tipos de relatório

### Todos com saldo (padrão)

Lista todos os lotes com fornecedor, fabricação, validade, saldo e filial. Use **Somente com saldo** para ocultar os zerados. Os filtros de produto, fornecedor e filial funcionam.

### Lotes a vencer

Informe os dias no campo **Dias** (padrão 30, máximo 3.650). A grade lista lotes com saldo cuja validade é igual ou anterior a hoje mais esses dias, na filial em que você está logado, do vencimento mais próximo ao mais distante. A coluna **Dias** mostra os dias até vencer.

!!! info "Lotes já vencidos também aparecem"
    A lista não tem limite inferior. Lote vencido aparece com **Dias** negativo ou zero.

![placeholder: grade Lotes a vencer com a coluna Dias destacada](img2.png)

### Lotes sem movimento

Informe os dias no campo **Dias** (padrão 90). A grade lista lotes com saldo, na filial atual, cujo último movimento efetivado foi há esse número de dias ou mais. A coluna **Dias sem mov** mostra há quanto tempo o lote está parado. Lote que nunca teve movimento efetivado não entra.

### Auditoria SP_ESTOQUE x saldo por lote

Compara o saldo do produto no estoque com a soma dos saldos dos lotes. Só aparecem produtos que controlam lote e têm diferença. Não usa filtro de dias nem de filial.

| Divergência | Significado |
|-------------|-------------|
| **Positiva** | O estoque tem mais do que os lotes somam. Falta lote de abertura ou ajuste manual |
| **Negativa** | Os lotes somam mais do que o estoque. Houve lote lançado a mais ou saída fora do controle de lote |

!!! tip "Quando rodar"
    Rode a auditoria depois de habilitar o controle de lote num produto com histórico, ou quando suspeitar de diferença entre estoque e lotes.

![placeholder: grade da auditoria com a coluna Divergencia destacada](img3.png)

---

## Alerta de lotes vencidos na abertura

Ao abrir o Factus, se a filial atual tiver lotes vencidos com saldo, a barra de status mostra no painel vermelho a mensagem **N lote(s) vencido(s) com saldo**. É o mesmo painel do aviso de nova versão.

!!! info "O alerta não bloqueia"
    Use o aviso como lembrete. Abra **Lotes a vencer** para ver os lotes vencidos e decidir sobre baixa, descarte ou ajuste.

![placeholder: barra de status com o aviso de lotes vencidos destacado](img4.png)

---

## Imprimir

O PDF sai em paisagem, com o título **Lotes de Produto** e o tipo escolhido, mais os filtros usados e o total de registros.

<!--
??? note "Referência técnica"

    Fonte: fontes/uCadLoteProduto.pas (TTipoRelatorioLote, MontaSQLPesquisa, FormataCamposPesquisa); alerta em fontes/uPrincipal.pas FormShow (ContarLotesVencidosComSaldo, StatusBar1.Panels[3])
    Dias: edtDiasRelatorio MaxValue 3650; valor <= 0 na consulta vira 30
    Auditoria: SP_ESTOQUE(pro, NULL) x VW_LOTE_PRODUTO_SALDO, só PRO_CONTROLA_LOTE = 'S'
    Permissão: 1 (msProdutos)
-->
