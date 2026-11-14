# Habilitando o Controle de Lote num Produto

Antes de rastrear lotes em compras, vendas ou produção, marque o produto para controlar lote. A opção fica no cadastro do produto e vale só para ele.

---

## Como acessar

**Produtos → Produtos e Serviços(Todos)**, e abra o produto. Para matéria-prima, use **Produtos → Matéria prima/insumos/embalagens**.

![placeholder: cadastro de produto com as opções Controla lote e Controla validade destacadas](img1.png)

---

## Permissões

| Permissão | Libera |
|-----------|--------|
| **Gravar produtos** (agrupador **Produtos**) | Salvar o cadastro com a opção marcada |
| **Lançar movimentação manual de estoque** (agrupador **Estoque**) | Criar o lote de abertura (passo 4) |

---

## Fluxo de uso

### 1. Marque "Controla lote"

No cadastro do produto, marque **Controla lote**. Daqui em diante, o sistema pede o lote sempre que o produto entra (compra ou produção) ou sai (venda ou consumo em produção).

### 2. Marque "Controla validade", se o produto vence

**Controla validade** só fica disponível com **Controla lote** marcado. Se você desmarcar **Controla lote**, o sistema desmarca **Controla validade** junto.

!!! info "Produto com lote e sem validade"
    O produto que controla só lote não precisa de data de vencimento. Você informa número do lote, fabricação e origem.

### 3. Salve o cadastro

Clique em **Salvar**. O controle passa a valer para o produto.

### 4. Crie o lote de abertura, se o produto já tem saldo

Ao salvar um produto que já existia, o sistema soma o saldo dele em estoque. Se houver saldo, pergunta:

> Produto tem saldo N em estoque atual. Deseja criar um lote de abertura para nao bloquear vendas futuras?

- **Sim**: abre a janela **Lote de abertura**. Confira os campos e clique em **Criar**.
- **Não**: nada acontece. O saldo antigo fica sem lote.

| Campo | Descrição |
|-------|-----------|
| **Numero do lote** | Vem sugerido como `ABERTURA-` e o ano atual (por exemplo `ABERTURA-2026`). Aceita até 20 caracteres |
| **Fabricacao** | Vem com a data de hoje |
| **Validade (opc.)** | Só aparece se o produto controla validade. Marque e informe uma data posterior a hoje |

![placeholder: janela Lote de abertura com Numero do lote, Fabricacao e Validade em destaque](img2.png)

O lote nasce com a quantidade do saldo total do produto e fica lançado na filial em que você está logado.

!!! warning "Sem lote de abertura, a venda trava"
    Se você recusar o lote de abertura, a venda do produto exige escolher um lote. Sem nenhum lote com saldo, a venda não tem de onde tirar a mercadoria. Cadastre um lote na tela [Lotes de Produto](lotes-de-produto.md) antes de vender.

!!! info "O saldo do estoque não muda"
    O lote de abertura só registra a origem das unidades que já existiam. O saldo em estoque continua o mesmo.

!!! info "Quando a pergunta aparece"
    A pergunta só aparece quando você salva um produto já cadastrado que passou a controlar lote naquela edição. Produto novo não dispara a pergunta. Desmarcar **Controla lote** também não.

---

## Limitações da versão atual

- A pergunta do lote de abertura soma o saldo do produto em todas as filiais, mas o lote é lançado só na filial atual.
- Se o usuário não tiver a permissão de movimentação manual de estoque, o lote de abertura não é criado.

<!--
??? note "Referência técnica"

    Fonte: fontes/uProdutos.pas / uProdutos.lfm (chkControlaLote, chkControlaValidade, AtualizarControleValidade, SugerirLoteAbertura); fontes/uCadLoteProduto.pas (AbrirModoAbertura)
    Menu: Produtos → Produtos e Serviços(Todos) / Matéria prima/insumos/embalagens
    Campos: PRODUTO.PRO_CONTROLA_LOTE, PRO_CONTROLA_VALIDADE (CHAR 'S'/'N')
    Saldo da pergunta: soma de SP_ESTOQUE(pro, null) (global); lote de abertura lançado em vFilial com LOTM_ABERTURA='S', sem MOV_MANUAL_PRODUTO
    Dispara em ExecutarAposCommitGravar, só em UPDATE com transição N → S (vControlaLoteInicial)
    Permissões: 2 = Gravar produtos (btnSalvar), 5 = Lançar movimentação manual de estoque (AbrirModoAbertura)
    Scripts SQL: 608, 609
-->
