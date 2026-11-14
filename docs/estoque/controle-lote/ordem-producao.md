# Consumo e Produção em Ordem de Produção

Na Ordem de Produção, o controle de lote registra dois pontos: o lote da matéria-prima consumida e o lote do produto acabado gerado ao encerrar a produção.

---

## Como acessar

**Produtos → PCP → Ordem de Produção**

![placeholder: menu Produtos, PCP, Ordem de Produção destacado](img1.png)

---

## Permissões

Valem as permissões de PCP. A tela exige **Consultar Ordem de Produção** (agrupador **PCP**).

---

## Fluxo de uso

### 1. Informe o lote consumido

Na lista de itens da atividade, selecione a matéria-prima e clique em **Consumir Lotes**. Abre a janela **Lote consumidos nos itens da ficha técnica**. Clique em novo e preencha:

| Campo | Descrição |
|-------|-----------|
| **Lote** | Número do lote de onde a matéria-prima sai |
| **Quantidade** | Quantidade consumida do lote |
| **Data Fabricado** | Opcional |
| **Data Validade** | Opcional |
| **Código Agregação** | Opcional |

Ao gravar, o consumo vira saída no lote, na filial da OP. Excluir a linha desfaz a saída.

![placeholder: janela de lotes consumidos com os campos Lote e Quantidade destacados](img2.png)

!!! info "Lote já encerrado"
    Se o lote da OP já foi encerrado, o sistema pergunta se você quer fazer a manutenção dos lotes consumidos.

!!! warning "Produto sem controle de lote"
    Se a matéria-prima não controla lote, o sistema avisa "Produto nao controla lote" e não abre a janela. Habilite antes em [Habilitando o controle de lote](habilitando.md).

!!! warning "Lote precisa existir"
    O número deve estar cadastrado para o produto, por compra, produção ou cadastro manual. Se não for encontrado, o sistema bloqueia a gravação.

!!! warning "Número repetido entre fornecedores"
    Se o mesmo número existe para mais de um fornecedor, o sistema bloqueia. Identifique o lote certo na tela [Lotes de Produto](lotes-de-produto.md).

### 2. Encerre o lote da OP

Clique com o botão direito no lote, na grade de lotes, e escolha **Finaliza Produção**. Confirme. Abre a janela **Encerramento de Lote**, com OP, produto e lote no topo. Ela tem até três etapas, e o botão muda de **Próximo** para **Encerrar** na última.

**Etapa Produção**

| Campo | Descrição |
|-------|-----------|
| **Data de fabricação** | Data que também gera a entrada de estoque |
| **Quantidade produzida** | Vem com a quantidade planejada do lote. Ajuste para o que foi produzido |
| **Validade** | Só aparece se o produto controla validade |

**Etapa Perdas** (só se o lote tem matéria-prima)

Informe a **Perda total (un.)** e clique em **Calcular perdas por material**. O sistema sugere planejado menos produzido e distribui pelas matérias-primas. Você pode corrigir **Consumido** e **Perda** de cada uma.

**Etapa Sub-produtos**

Escolha o produto, informe **Qtd:** e clique em **Adicionar**. Use **Remover selecionado** para tirar uma linha.

![placeholder: janela Encerramento de Lote com Data de fabricação, Quantidade produzida e Validade destacados](img3.png)

Se o produto da OP controla lote, o sistema cria um lote de produção com o número do lote da OP, a quantidade e a data informadas.

!!! warning "Coerência de datas"
    A fabricação não pode ser anterior à saída das matérias-primas. Se for, o sistema pergunta se você quer ajustar a data de saída para a data de fabricação.

!!! warning "Validade antes da fabricação"
    O sistema bloqueia validade anterior à data de fabricação.

!!! warning "Fechamento de estoque no dia"
    Se o produto da OP tem fechamento de estoque na data de hoje, o sistema não deixa finalizar o lote.

---

## Limitações da versão atual

- Não existe rotina para reabrir uma OP encerrada e desfazer o lote de produção. Peça apoio ao suporte.

<!--
??? note "Referência técnica"

    Fonte: fontes/uLoteValidade.pas (TfrmLoteValidade, SincronizarLedgerConsumoItemOP, ResolverLoteConsumo), fontes/PCP/uEncerramentoLoteOP.pas, fontes/PCP/uPCPOrdem_Producao.pas (AlterarStatusLote, btnConsumirLoteClick)
    Menu: Produtos → PCP → Ordem de Produção (MenuItem13)
    Tabelas: PCP_LOTE_ITENS_ATV_OP, PCP_LOTE_OP (PCPLOP_ENTRADA_ESTOQUE, PCPLOP_QTD_ENTRADA, PCPLOP_VALIDADE, PCPLOP_DATA_ENCERRADO), pcp_lote_op_subproduto, LOTE_PRODUTO_MOV (PCPLIOP_CODIGO consumo, PCPLOP_CODIGO produção)
    A janela de encerramento abre para qualquer produto; o lote só é criado se PRO_CONTROLA_LOTE = 'S'
    Permissão: 31 (msPCP)
-->
