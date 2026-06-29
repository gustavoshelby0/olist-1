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


1. Dimensão Cliente
   
Fornece detalhes sobre quem está comprando.

Coluna na Fonte	Nome no Modelo	Descrição

customer_id	ID_Cliente	Chave Primária (PK) da dimensão.

customer_unique_id	ID_Cliente_Unico	Identificador único do cliente para toda a base.

customer_zip_code_prefix	FK_Geo_Cliente	Chave estrangeira para localização (Geolocation).


2. Dimensão Geolocalização
   
Usada para localizar clientes e vendedores (Snowflake - ligação indireta).

Coluna na Fonte	Nome no Modelo	Descrição

geolocation_zip_code_prefix	ID_Geo	Chave Primária (PK) - CEP de prefixo.

geolocation_lat	Latitude	Coordenada geográfica.

geolocation_lng	Longitude	Coordenada geográfica.

geolocation_city	Cidade	Nome da cidade.

geolocation_state	Estado	Sigla do estado (UF).

3. Dimensão Pedido (Cabeçalho)
   
Agrupa os itens e contém informações do status geral da compra.

Coluna na Fonte	Nome no Modelo	Descrição

order_id	ID_Pedido	Chave Primária (PK).

customer_id	FK_Cliente	Chave estrangeira para o Cliente que fez o pedido.

order_status	Status_Pedido	Situação atual (ex: delivered, shipped, canceled).

order_purchase_timestamp	FK_Data_Compra	Chave estrangeira para Dimensão Tempo (Data da compra).

order_approved_at	FK_Data_Aprovacao	Chave para Tempo (Data de aprovação do pagamento).

order_delivered_carrier_date	FK_Data_Envio_Transp	Chave para Tempo (Data de postagem no transportador).

order_delivered_customer_date	FK_Data_Entrega	Chave para Tempo (Data de entrega ao cliente).

order_estimated_delivery_date	FK_Data_Prevista	Chave para Tempo (Data prevista de entrega).

4. Dimensão Produto
   
Descreve as características físicas e de categorização do item.

Coluna na Fonte	Nome no Modelo	Descrição

product_id	ID_Produto	Chave Primária (PK).

product_category_name	FK_Categoria	Chave estrangeira para a Dimensão Categoria (idioma PT).

product_name_lenght	Tamanho_Nome	Número de caracteres do nome.

product_description_lenght	Tamanho_Desc	Número de caracteres da descrição.

product_photos_qty	Qtd_Fotos	Quantidade de imagens do produto.

product_weight_g	Peso_g	Peso em gramas.

product_length_cm	Comprimento_cm	Dimensão física do produto.

product_height_cm	Altura_cm	Dimensão física do produto.

product_width_cm	Largura_cm	Dimensão física do produto.

5. Dimensão Categoria (Tradução)
   
Tabela auxiliar para descrever a categoria em Inglês.

Coluna na Fonte	Nome no Modelo	Descrição

product_category_name	ID_Categoria_PT	Chave Primária (PK) - Nome em Português.

product_category_name_english	Categoria_EN	Tradução para o Inglês (útil para dashboards).

6. Dimensão Vendedor

Fornece dados sobre o lojista que está vendendo o produto.

Coluna na Fonte	Nome no Modelo	Descrição

seller_id	ID_Vendedor	Chave Primária (PK).

seller_zip_code_prefix	FK_Geo_Vendedor	Chave estrangeira para localização (Geolocation).

seller_city	Cidade_Vendedor	Cidade do vendedor (denormalizado).

seller_state	Estado_Vendedor	Estado do vendedor (denormalizado).

7. Dimensão Pagamento
Detalha como foi pago o pedido (pode ter múltiplas linhas por pedido).

Coluna na Fonte	Nome no Modelo	Descrição

order_id	FK_Order	Chave estrangeira ligada ao Pedido.

payment_sequential	Sequencia_Pag	Número da parcela/sequência (PK composta com Order).

payment_type	Tipo_Pagamento	Método (ex: credit_card, boleto, voucher).

payment_installments	Qtd_Parcelas	Número total de parcelas.

payment_value	Valor_Parcela	Medida: Valor pago naquela transação específica.

8. Dimensão Avaliação (Review)

Contém a nota e comentários sobre a experiência do pedido.

Coluna na Fonte	Nome no Modelo	Descrição

review_id	ID_Avaliacao	Chave Primária (PK).

order_id	FK_Order	Chave estrangeira para o Pedido.

review_score	Nota	Atributo: Nota de 1 a 5.

review_comment_title	Titulo_Coment	Título do comentário.

review_comment_message	Mensagem	Texto completo da avaliação.

review_creation_date	FK_Data_Criacao	Chave para Tempo (Data que a avaliação foi criada).

review_answer_timestamp	FK_Data_Resposta	Chave para Tempo (Data que o vendedor respondeu).

9. Dimensão Tempo (Derivada)

Criada para análises temporais. Extraída das colunas com _timestamp ou _date.

Coluna no Modelo	Descrição

ID_Data	Chave Primária (ex: AAAAMMDD).

Data_Completa	Data no formato padrão (YYYY-MM-DD).

Ano	Extraído da data.

Mes	Extraído da data.

Mes_Nome	Nome do mês (ex: Janeiro).

Trimestre	Número do trimestre (1 a 4).

Dia_Semana	Nome do dia da semana.

Final_de_Semana?	Flag (Sim/Não) para dias de Sábado e Domingo.


## Passo 5: Combinação Fato-Dimensão

**Mind Map – Direcionadores de Análise**

Para orientar a exploração dos dados, mesmo sendo um analista novo no setor, foram mapeados os seguintes grupos de perguntas:


### **Dimensão 1: Tempo (Datas de Compra, Envio e Entrega)**

*Base: colunas de timestamp da Dimensão Pedido e da Fato.*

1. **Qtd de Pedidos por Mês** (data da compra – `order_purchase_timestamp`).
2. **Valor Total de Vendas (`SUM(price)`) por Trimestre** (data da compra).
3. **Qtd de Itens Vendidos por Dia da Semana** (data da compra – ex: seg, ter...).
4. **Qtd de Pedidos por Mês de Envio** (data limite de envio – `shipping_limit_date` da Fato).
5. **Ticket Médio (`SUM(price)/COUNT(DISTINCT order_id)`) por Ano** (data da compra).

---

### **Dimensão 2: Cliente (Quem Comprou)**

*Base: `customer_id`, `customer_unique_id` e geolocalização ligada.*

1. **Qtd de Pedidos por Estado do Cliente** (via `geolocation_state`).
2. **Valor Total de Vendas por Cidade do Cliente** (via `geolocation_city`).
3. **Qtd de Itens Comprados por Cliente** (Ranking dos Top 10).
4. **Valor Médio de Frete (`AVG(freight_value)`) por Cliente**.
5. **Qtd de Pedidos por Faixa de CEP** (agrupando os 3 primeiros dígitos do `zip_code_prefix`).

---

### **Dimensão 3: Geolocalização (Localização do Cliente/Vendedor)**

*Base: `geolocation_zip_code_prefix` (tabela auxiliar para enriquecer localização).*

1. **Qtd de Pedidos por Região do Brasil** (agrupar `geolocation_state` em Sul, Sudeste, Centro-Oeste, Norte, Nordeste).
2. **Valor Total de Vendas por Estado** (do cliente).
3. **Qtd de Pedidos por Cidade** (do cliente – lista das Top 10).
4. **Comparativo: Qtd de Pedidos por Estado do Cliente vs. Estado do Vendedor** (cruzamento indireto entre duas localizações).
5. **Valor Total de Frete por Estado do Cliente** (para ver onde o frete é mais caro).

---

### **Dimensão 4: Produto (O que foi Vendido)**

*Base: `product_id` e seus atributos físicos.*

1. **Qtd de Itens Vendidos por Produto** (Top 10 produtos mais vendidos).
2. **Valor Total de Vendas por Produto** (Ranking de faturamento).
3. **Preço Médio Unitário (`AVG(price)`) por Produto**.
4. **Qtd de Pedidos que contêm determinado Produto** (popularidade em pedidos distintos).
5. **Correlação / Média de Frete por Faixa de Peso do Produto** (agrupar `product_weight_g` em categorias: Leve, Médio, Pesado).

---

### **Dimensão 5: Categoria (Tradução e Agrupamento de Produtos)**

*Base: `product_category_name` + tabela de tradução para Inglês.*

1. **Qtd de Itens Vendidos por Categoria** (nome em Português).
2. **Valor Total de Vendas por Categoria** (nome em Inglês – para dashboards).
3. **Ticket Médio por Categoria** (média de preço por pedido dentro da categoria).
4. **Média de Avaliação (`AVG(review_score)`) por Categoria** (quais categorias são melhor avaliadas).
5. **Qtd de Pedidos com Atraso na Entrega por Categoria** (cruzando com flag de atraso da Dimensão Pedido).

---

### **Dimensão 6: Vendedor (Lojista)**

*Base: `seller_id` e sua localização.*

1. **Qtd de Itens Vendidos por Vendedor** (volume de vendas).
2. **Valor Total de Vendas por Vendedor** (faturamento).
3. **Valor Total de Frete Cobrado por Vendedor** (soma do frete dos itens dele).
4. **Média de Preço dos Produtos do Vendedor** (se vende itens caros ou baratos).
5. **Qtd de Pedidos Atendidos por Vendedor** (quantos pedidos distintos ele participou).

---

### **Dimensão 7: Pedido (Cabeçalho - Status e Prazos)**

*Base: `order_id`, `order_status`, datas de entrega vs estimada.*

1. **Qtd de Pedidos por Status** (`delivered`, `shipped`, `canceled`, etc.).
2. **Qtd de Pedidos Entregues com Atraso** vs. **Entregues no Prazo** (comparar `order_delivered_customer_date` com `order_estimated_delivery_date`).
3. **Valor Total de Vendas por Status do Pedido** (faturamento por situação).
4. **Média de Dias para Entrega** (do `order_purchase_timestamp` ao `order_delivered_customer_date`) por Status.
5. **Qtd de Pedidos Cancelados por Mês** (série temporal de cancelamentos).

---

### **Dimensão 8: Pagamento (Forma e Parcelamento)**

*Base: `payment_type`, `payment_installments`, `payment_value`.*

1. **Qtd de Pedidos por Tipo de Pagamento** (`credit_card`, `boleto`, `voucher`, etc.).
2. **Valor Total de Vendas por Tipo de Pagamento** (faturamento por método).
3. **Média de Parcelas (`AVG(payment_installments)`) por Tipo de Pagamento**.
4. **Qtd de Pedidos com Pagamento à Vista** (1 parcela) vs. **Parcelado** (>1 parcela).
5. **Valor Médio do Pedido por Faixa de Parcelas** (ex: 1 parcela, 2 a 6, 7 ou mais).

---

### **Dimensão 9: Avaliação (Review e Notas)**

*Base: `review_score`, comentários e datas de criação/resposta.*

1. **Qtd de Pedidos por Nota** (distribuição das notas 1, 2, 3, 4, 5).
2. **Valor Total de Vendas por Faixa de Nota** (Baixa = 1-2, Média = 3, Alta = 4-5).
3. **Média de Preço dos Itens por Nota** (clientes que dão nota alta gastam mais?).
4. **Qtd de Comentários com Texto Preenchido** (`review_comment_message IS NOT NULL`) por Nota.
5. **Tempo Médio (em dias) entre a Data de Entrega e a Data da Avaliação** (`review_creation_date`) por Nota (clientes que avaliam rápido dão notas melhores?).


## Passo 6: Escolha dos Gráficos

Este projeto foi reorganizado após a criação dos painéis no Power BI. Por esse motivo, a modelagem fato-dimensão apresentada, bem como a escolha dos gráficos associados a essa coluna, possui caráter ilustrativo e foi adaptada apenas para fins de documentação.

A reorganização completa da modelagem e da seleção dos gráficos não foi realizada, pois o projeto é composto por aproximadamente nove painéis, o que tornaria esse processo desnecessariamente extenso.

## Passo 7: Painel Macro-Micro




# Resultados

**📥 Baixe todos os paineis da Olist (clique no link e, em seguida, em "Download" ou "View raw"):**  
[https://drive.google.com/file/d/1IKfGu8_IAGmM31BCFYhJILYpoZmQ6201/view?usp=sharing](https://drive.google.com/file/d/1IKfGu8_IAGmM31BCFYhJILYpoZmQ6201/view?usp=sharing)

# Próximos passos

Obter o feedback do CEO para realizar análises mais profundas, considerando os novos questionamentos que provavelmente serão levantados. Em outras palavras, realizar análises diagnósticas para cada área da empresa.
