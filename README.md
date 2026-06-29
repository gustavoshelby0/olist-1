## Análise da SuperStore RFM & Cohort & Descriptive

# Problema de Negócio

Você foi contratado pela empresa **Olist** como Analista de Dados Júnior.

A Olist é uma empresa brasileira de e-commerce que começou a crescer rapidamente. Porém, até então, a maioria das decisões era tomada pelo corpo diretivo de forma intuitiva, sem análises aprofundadas e sem o apoio de indicadores confiáveis. Como consequência da falta de uma cultura orientada por dados, a empresa tomou algumas decisões equivocadas que resultaram em prejuízos.

Para que a empresa continue crescendo de forma saudável, o CEO, que se sente "cego" em relação aos dados do negócio, decidiu implementar uma estratégia de **Business Intelligence (BI)** com o objetivo de criar indicadores que apoiem a tomada de decisões. Diante dos prejuízos identificados, foi estabelecido que a empresa deixará de se basear em suposições e passará a adotar uma cultura **Data Driven** na tomada de decisões estratégicas.

Considerando o melhor custo-benefício, a ferramenta escolhida pelo corpo diretivo foi o **Power BI**.

O CEO decidiu que as análises serão desenvolvidas por frentes de negócio. Assim, ao final de cada entrega, uma nova frente será solicitada ao Analista de Dados. Inicialmente, todo o desenvolvimento deverá ser realizado no **Power BI Desktop**.

As frentes de análise serão desenvolvidas na seguinte ordem:

- Produto
- Pagamentos
- Pedidos
- Avaliações
- Vendedores
- Vendas

**Importante:** o CEO deixou claro que aceitará, no máximo, **dois painéis por visão**.

## Primeira tarefa

Sua primeira missão como membro da equipe é desenvolver a **Visão Produto**.

Durante a reunião com o CEO, foram definidas as seguintes solicitações de análise:

- Quantidade total de produtos cadastrados;
- Quantidade total de categorias;
- Quantidade total de fotos;
- Quantidade de produtos por categoria;
- Quantidade de fotos por categoria.

Além disso, o CEO solicitou que o dashboard utilize as **cores padrão da empresa** e possua um **filtro por categoria de produto**.

# Premissas da análise

- Dados de 9.994 vendas feitas pela SuperStore.
- Vendas realizadas nos Estados Unidos.
- Os dados analisados correspondem ao período de 2014 a 2018.

# Estratégia da solução

O método Fato-Dimensão foi usado para desenvolver a análise de dados.

# Análise Descritiva

## Passo 1: Resumir o contexto em uma pergunta aberta

As perguntas abertas são um tipo de demanda muito comum em análise de dados nas quais a demanda possui N possíveis soluções e cabe ao analista de dados avaliar as possibilidades e escolher a alternativa com o maior retorno e o menor esforço possível. Para essa análise, foi definida a seguinte pergunta aberta:

*Como estão as vendas da SuperStore? A empresa está dando lucro? Há um crescimento no número de clientes e compras ao longo do tempo?*

## Passo 2: Transformar pergunta aberta em fechada

As perguntas fechadas são um tipo de demanda muito comum na área de análise de dados. Essa demanda contém todos os detalhes da análise de dados e direciona o analista exatamente para o que precisa ser feito. Geralmente, a pergunta fechada é a escolha de uma solução entre todas as alternativas possíveis, feita por um profissional mais sênior da área.

Para essa análise, foi definida a seguinte pergunta fechada:

**Pergunta Fechada:** Faça uma análise das vendas da SuperStore, veja qual categoria está dentro da lei de Pareto (80-20), como estão o número de clientes, o número de pedidos, ele está aumentando? Estagnou? Quais categorias não trazem retorno para a SuperStore? Faça a análise com o gráfico de Pareto.

## Passo 3: Definição da Coluna Fato

O Fato é a coluna de interesse que representa o ponto focal da análise. Nesse caso, a coluna "OrderID" mostra quantas vendas foram feitas, quando, é feita uma contagem e feito uma segmentação por categoria...

## Passo 4: Identificação das Dimensões

As colunas foram agrupadas em dimensões comuns que fornecem mais detalhes sobre o Fato que será analisado. Foram organizadas as seguintes dimensões:

| Dimensão | Colunas |
| :--- | :--- |
| Tempo (Datas do Pedido e Envio) | Order Date, Ship Date (a partir delas, pode-se extrair: order_year, order_month, order_quarter, ship_year, ship_month) |
| Cliente (Quem Comprou) | Customer ID, Customer Name, Segment, Country, City, State, Postal Code, Region |
| Produto (O que Foi Vendido) | Product ID, Category, Sub-Category, Product Name |
| Pedido (Cabeçalho da Transação) | Order ID, Ship Mode (modo de frete/entrega) |
| Item do Pedido (Linha/Detalhe do Fato) | Row ID (identificador único de cada linha do pedido), Sales (valor da venda), Quantity (quantidade), Discount (desconto aplicado), Profit (lucro) |

## Passo 5: Combinação Fato-Dimensão

**Mind Map – Direcionadores de Análise**

Para orientar a exploração dos dados, mesmo sendo um analista novo no setor, foram mapeados os seguintes grupos de perguntas:

- Quantidade de Pedidos por Data (Mês)
- Quantidade de Pedidos por Data de Envio (Mês)
- Quantidade de Pedidos por Tier de Preço (Baixo, Médio, Alto)
- Quantidade de Pedidos por Quantidade de Itens
- Quantidade de Pedidos por Tier de Desconto (Baixo, Médio, Alto)
- Quantidade de Pedidos por Produto
- Quantidade de Pedidos por Clientes
- Quantidade de Pedidos por Data e Tier de Preço (Baixo, Médio, Alto)
- Quantidade de Pedidos por Data e Quantidade de Itens
- Quantidade de Pedidos por Data e Produto
- Quantidade de Pedidos por Data e Clientes
- Quantidade de Pedidos por Data de Envio e Tier de Preço

## Passo 6: Escolha dos Gráficos

- [x] Quantidade de Pedidos por Data (Mês) - Gráfico de Linhas
- [x] Desenhar o gráfico de Quantidade de Clientes Únicos
- [x] Quantidade de Pedidos por Cliente
- [x] Quantidade de Pedidos por Itens
- [x] Desenhar o gráfico de Distribuição de Pedidos por Produto

## Passo 7: Painel Macro-Micro

[https://img.notionusercontent.com/s3/prod-files-secure%2F2b76fb90-3276-8107-9a2b-0003db8f3f1b%2F559e753e-ca94-4d58-97e5-2cf9018ed757%2FCapturar.png/size/w=2000?exp=1782695552&sig=WhAahVMGwk-4q-j_K8-f3v_bZCRHuSz-Lx-xrUz4v6k&imgBuildSrc=presignImageUrl&id=38e6fb90-3276-8076-b420-e1499e5d1c32&table=block&userId=2cdd872b-594c-8197-aa3d-0002004cefb4&mtd=com](https://img.notionusercontent.com/s3/prod-files-secure%2F2b76fb90-3276-8107-9a2b-0003db8f3f1b%2F559e753e-ca94-4d58-97e5-2cf9018ed757%2FCapturar.png/size/w=2000?exp=1782695552&sig=WhAahVMGwk-4q-j_K8-f3v_bZCRHuSz-Lx-xrUz4v6k&imgBuildSrc=presignImageUrl&id=38e6fb90-3276-8076-b420-e1499e5d1c32&table=block&userId=2cdd872b-594c-8197-aa3d-0002004cefb4&mtd=com)


# Resultados

**📥 Baixe o gráfico no Excel com toda análise descritiva & cohort & rfm (clique no link e, em seguida, em "Download" ou "View raw"):**  
[https://docs.google.com/spreadsheets/d/1KP8CIZnk1aWoTs4k4oS6yJi1f8BWoemB/edit?usp=sharing&ouid=114029927907630112086&rtpof=true&sd=true](https://docs.google.com/spreadsheets/d/1KP8CIZnk1aWoTs4k4oS6yJi1f8BWoemB/edit?usp=sharing&ouid=114029927907630112086&rtpof=true&sd=true)

# Próximos passos

**Passo 1 – Recalcular a segmentação RFM substituindo a coluna "Monetização" pela coluna "Profit" (Lucro):** Os dados atuais de monetização mostram que Risco e Fies faturam R$ 12,13 bi. Porém, o dataset contém a coluna Discount e Profit. É necessário verificar se esses segmentos mantêm a liderança quando a métrica é lucro líquido, ou se os descontos concedidos corroem essa vantagem.

**Passo 2 – Cruzar a lista de produtos/categorias do Pareto (80/20) com os segmentos RFM:** Os dados de vendas estão detalhados por Category e Sub-Category. Deve-se identificar quais categorias estão no topo do Pareto para o segmento "Risco" e quais estão no topo para o segmento "Fies". Se houver divergência, a estratégia de estoque e cross-sell deve ser segmentada por perfil de cliente.

**Passo 3 – Calcular o tempo médio entre compras (intervalo) para os segmentos "Risco" e "Fies":** A coorte mostra picos de recompra nos meses 11, 17 e 22. Deve-se calcular, para cada Customer ID desses segmentos, a mediana dos dias entre uma compra e outra. Se a mediana for consistente com 150-180 dias, a janela de reativação deve ser ajustada para D+150 (e não D+60 ou D+90).

**Passo 4 – Medir o impacto do desconto (Discount) na retenção por coorte:** Os dados contêm a coluna Discount. Deve-se segmentar a coorte de Janeiro/2014 entre clientes que receberam desconto > 15% e clientes com desconto ≤ 5%, e comparar as taxas de recompra no mês 11. Se a taxa for significativamente menor no grupo com alto desconto, a política de descontos deve ser revisada para aquisição de novos clientes.

**Passo 5 – Construir um comparativo de ROI por canal/janela temporal:** Com base nas janelas de gelo (meses 2, 5, 8) e de ouro (meses 10, 16, 21), deve-se calcular o custo médio por contato (e-mail/SMS/WhatsApp) e o retorno médio por cliente reativado em cada período. O período que apresentar maior razão retorno/custo deve receber prioridade orçamentária nos próximos ciclos.
