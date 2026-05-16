# Regras de Conciliação

As regras de conciliação permitem automatizar o processo de conciliação bancária, associando automaticamente lançamentos do extrato bancário aos registros financeiros do sistema.

## O que são regras de conciliação?

Uma regra define critérios que, quando satisfeitos, associam automaticamente um lançamento bancário a um tipo de registro no sistema — eliminando a necessidade de conciliação manual.

## Como acessar

**Financeiro → Conciliação Bancária → Regras de Conciliação**

## Criando uma regra

1. Clique em **Nova Regra**
2. Preencha os campos:

| Campo | Descrição |
|---|---|
| Nome | Identificação da regra |
| Condição | Critério de correspondência (ex: descrição contém "PIX RECEBIDO") |
| Ação | O que fazer ao identificar o lançamento |
| Conta contábil | Conta a ser debitada/creditada |
| Ativo | Liga ou desliga a regra |

3. Clique em **Salvar**

## Tipos de condição

- **Descrição contém** — verifica se o histórico do extrato contém um texto
- **Valor igual a** — associa por valor exato
- **Valor entre** — associa lançamentos dentro de uma faixa de valor
- **Tipo de lançamento** — crédito ou débito

## Exemplo prático

!!! example "Regra: PIX de clientes"
    - **Condição:** descrição contém `PIX`  e tipo = `Crédito`
    - **Ação:** Lançar como recebimento de cliente
    - **Conta:** Clientes a Receber

## Ordem de prioridade

Quando mais de uma regra se aplica ao mesmo lançamento, o sistema usa a **ordem de cadastro** como prioridade. Reordene as regras arrastando pelo ícone à esquerda.

!!! warning "Atenção"
    Regras muito genéricas podem conciliar lançamentos incorretamente. Sempre teste uma regra nova com extratos reais antes de ativá-la definitivamente.
