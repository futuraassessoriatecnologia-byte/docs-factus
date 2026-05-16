Como gerar uma nota fiscal de exportação

Sistema deve atualizado com versão 24.11.20.00 ou superior.

1 - Cadastre um novo estado com EX, menu Parceiros → Cadastros → Estados.

![Imagem](../assets/nfe/image1.png)

2 - Cadastre a cidade, informando a UF como EX, e informe o código do país(4 dígitos) e o nome do país,  menu Parceiros → Cadastros → Cidades.

![Imagem](../assets/nfe/image2.png)

3 - Cadastre o destinatário informando a cidade cadastrada. No campo IE, informe a identificação do estrangeiro, no CEP pode ser informado o CEP ou zeros.

![Imagem](../assets/nfe/image3.png)

4 - Crie a variação fiscal para ICMS, no exemplo foi usado CFOP 7.101, e CST 300

![Imagem](../assets/nfe/image4.png)

5 - Ao iniciar a digitação da nota fiscal, informando o cliente e a CFOP de exportação (inicia com 7), vai ativar a opção “Exportação”, os dois primeiros campos são obrigatórios(UF de Embarque e Descrição local embarque)

![Imagem](../assets/nfe/image5.png)

6 - Na exportação, alguns NCM tem a necessidade de enviar na unidade tributável um padrão de exigência, informar no campo abaixo no cadastro do produto qual unidade utilizar, será convertido somente a unidade. (Rejeição 817 - Unidade Tributavel incompativel com o NCM informado na operacao com Comercio Exterior [nItem:1] )

![Imagem](../assets/nfe/image6.png)