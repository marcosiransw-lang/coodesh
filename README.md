# DBA Challenge 20240802


## Introdução

Nesse desafio trabalharemos utilizando a base de dados da empresa Bike Stores Inc com o objetivo de obter métricas relevantes para equipe de Marketing e Comercial.

Com isso, teremos que trabalhar com várioas consultas utilizando conceitos como `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `GROUP BY` e `COUNT`.

### Antes de começar
 
- O projeto deve utilizar a Linguagem específica na avaliação. Por exempo: SQL, T-SQL, PL/SQL e PSQL;
- Considere como deadline da avaliação a partir do início do teste. Caso tenha sido convidado a realizar o teste e não seja possível concluir dentro deste período, avise a pessoa que o convidou para receber instruções sobre o que fazer.
- Documentar todo o processo de investigação para o desenvolvimento da atividade (README.md no seu repositório); os resultados destas tarefas são tão importantes do que o seu processo de pensamento e decisões à medida que as completa, por isso tente documentar e apresentar os seus hipóteses e decisões na medida do possível.
 
 

## O projeto

- Criar as consultas utilizando a linguagem escolhida;
- Entregar o código gerado do Teste.

### Modelo de Dados:

Para entender o modelo, revisar o diagrama a seguir:

![<img src="samples/model.png" height="500" alt="Modelo" title="Modelo"/>](samples/model.png)


## Selects

Construir as seguintes consultas:

- Listar todos Clientes que não tenham realizado uma compra;
- Listar os Produtos que não tenham sido comprados
- Listar os Produtos sem Estoque;
- Agrupar a quantidade de vendas que uma determinada Marca por Loja. 
- Listar os Funcionarios que não estejam relacionados a um Pedido.

## Readme do Repositório

- Deve conter o título do projeto
- Uma descrição sobre o projeto em frase
- Deve conter uma lista com linguagem, framework e/ou tecnologias usadas
- Como instalar e usar o projeto (instruções)
- Não esqueça o [.gitignore](https://www.toptal.com/developers/gitignore)
- Se está usando github pessoal, referencie que é um challenge by coodesh:  

>  This is a challenge by [Coodesh](https://coodesh.com/)

## Finalização e Instruções para a Apresentação

1. Adicione o link do repositório com a sua solução no teste
2. Verifique se o Readme está bom e faça o commit final em seu repositório;
3. Envie e aguarde as instruções para seguir. Caso o teste tenha apresentação de vídeo, dentro da tela de entrega será possível gravar após adicionar o link do repositório. Sucesso e boa sorte. =)


## Suporte

Para tirar dúvidas sobre o processo envie uma mensagem diretamente a um especialista no chat da plataforma. 


## Respostas às requisições propostas no desafio:

/* Listar todos Clientes que não tenham realizado uma compra */
/* Desconhecendo o domínio do campo order_status, não é possível considerar que alguém não realizou uma compra caso sua compra tenha status de cancelada. */
/* Sendo assim, a seleção considerará que qualquer ordem de compra registrada, independentemente do status, será considerada uma compra realizada. */
select C.first_name,
       C.last_name,
       C.phone,
       C.email,
       C.street,
       C.city,
       C.state,
       C.zip_code
from   customers   C
where  not exists( select 1
                   from   orders    O
                   where  O.customer_id = C.customer_id
                 )
order by
       C.state,
       C.city,
       C.first_name,
       C.last_name



/* Listar os Produtos que não tenham sido comprados */
/* A seleção não considera o status (order_status) de ordens de compra que tenham sido eventualmente canceladas */
select Ct.category_name,
       B.brand_name,
       P.product_name,
       P.model_year,
       P.list_price
from   products   P,
       brands     B,
       categories Ct
where  B.brand_id       = P.brand_id
  and  Ct.category_id   = P.category_id
  and  not exists( select 1
                   from   order_items  OI
                   where  OI.product_id = P.product_id
                 )
order by
       Ct.category_name,
       B.brand_name,
       P.product_name,
       P.model_year



/* Listar os Produtos sem Estoque */




