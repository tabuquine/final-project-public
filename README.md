# Aprendizado de Máquina aplicado ao Varejo

#### Aluno: [Marcos Tabuquine Marques](https://github.com/tabuquine)
#### Orientador: [Felipe Borges](https://github.com/FelipeBorgesC)

---

Trabalho apresentado ao curso [BI MASTER](https://ica.puc-rio.ai/bi-master) como pré-requisito para conclusão de curso e obtenção de crédito na disciplina "Projetos de Sistemas Inteligentes de Apoio à Decisão".

- Códigos: "Ingestão e Transformação de Dados.ipynb" (https://github.com/tabuquine/bimaster-projeto-final/blob/d7bc9d726d2c499e24fcacaddb39e9351e96bf18/Ingest%C3%A3o%20e%20Transforma%C3%A7%C3%A3o%20de%20Dados.ipynb) e "Analises Bases Varejo.ipynb" (https://github.com/tabuquine/bimaster-projeto-final/blob/5cc469ea1e089385f9ae6a54b62ec8a9f8386219/Analises%20Bases%20Varejo.ipynb)
- Repositório de Dados: https://drive.google.com/drive/folders/1--CfCpk_5w3TOAtwUBuC4jKQyFHSgAEM?usp=sharing

---

### Resumo

Este estudo tem como inspiração e objetivo, provar que uma abordagem de aprendizado de máquina a partir de dados de compra de cliente identificados, permite compreender padrões de comportamento de consumo para esses cliente e consequentemente tomar ações mais eficazes de promoções no Varejo.

A hipótese que será verificada é que sendo os clientes identificados, será possível agrupá-los através de dimensões de medida de comportamento, sendo elas a Recência, Frequência e Valor Monetário. E provada essa hipótese a próxima etapa seria entender através de regras de associações quais seriam as combinações de ofertas para os produtos mais relevantes a cada segmento.

O potencial de aplicação dessas informações para a empresa de Marketing Digital seria o de promover através de promoções customizadas por perfil de clientes a maior frequência de compra e o aumento do ticket médio, usando essa base e uma abordagem de aprendizado de máquina.

NOTA: Por motivos legais e de proteção de dados não foi usada nenhuma informação pessoal das pessoas, portanto a abordagem usará fundamentalmente o que esses consumidores estão comprando, com que frequência, etc, usando seus IDs unicos como chave de busca.

### 1. Introdução

Os dados obtidos para esse estudo foram cedidos por uma empresa de marketing digital que presta serviços para o pequenos e médios varejos de alimentos. O sample contém 6 meses de transações de compra para uma base de consumidores que são identificados no ato da compra através de seus CPFs e na base de dados ganharam um ID unico. Essas compras são feitas em 3 lojas de um mercado tipo hortifruti. O arquivo CSV possui cerca de 1GB.

As dimensões presentes no dataset são: ID da transação que identifica os itens de uma mesma compra (cesta), ID dos clientes que identifica as compras por cliente, o código e a descrição dos produtos comprados, assim como o valor unitário e a quantidade de produtos comprados e outras dimensões que não serão usadas para o estudo, como cupom de desconto, valor total da compra (será calculado) e desconto.

Portanto a primeira foi o carregamento das dimensões da base de dados, com a correspondente transformação desses dados, criando um dataframe com apenas as dimensões necssárias para o estudo (Ingestão e Transformação de Dados.ipynb)

### 2. Modelagem

A segunda etapa será a construção de novas dimensões (engenharia de features) para que se possibilite o agrupamento dos clientes do varejo pelos seus padrões de comportamento. Para essa etapa foi escolhido o conceito de análise RFM que é muito conhecido e aplicado no varejo para a categorização dos clientes.

A análise RFM permite uma comparação entre clientes quanto a Recência que seria uma medida de tempo para retorno, quanto a frequência das transações de cada cliente (e.g. identificação de clientes fiéis), e o valor monetário, que é a medida de quanto cada cliente gasta. Por exemplo, uma inclinação natural é dar mais ênfase ao incentivo aos clientes que gastam mais dinheiro ou aos mais frequentes.

Após a criação dessas dimensões para os clientes, será aplicado o k-means (https://en.wikipedia.org/wiki/K-means_clustering) como método de clusterização (agrupamento) dos clientes segundo as caracteristicas dessas 3 dimensões (RFM). Identificando então os principais grupos de clientes e suas caracteristicas, permitindo a empresa de Marketing entender seus clientes quanto essas dimensões e adotando para cada segmento a estratégia mais adequada segundo o propósito de negócio.

A terceira e ultima etapa será criar uma análise de cesta de compra para os clusters de interesse. Essa análise será feita usando um algoritmo de regras de associação, chamado Apriori (https://www.geeksforgeeks.org/apriori-algorithm/), conhecido e usado para esse propósito de análise. Para o objetivo desse estudo, usaremos o cluster de maior frequência, simulando então a intenção de aumentar o ticket médio deste grupo através de ofertas relevantes.

Para a análise de cesta de compra será usado o algoritmo Apriori. O objetivo será entender as associações mais relevantes para esse grupo, compreendendo que produtos deveriam ser priorizados em "combos" de promoção.

### 3. Resultados

Ao final das clusterizações RFM foi possível segmentar os clientes muito claramente quanto as suas caracteristicas em quatro clusters. O Cluster 2, apresenta uma alta frequência de compra, porém entre os clusters, menor ticket e recência. Esse tipo de comportamento é interpretado pelo varejo como o cliente solteiro ou casal, e/ou que mora perto da loja, e que faz suas compras a medida que vai surgindo a necessidade de consumo.

Em contrapartida, o Cluster 1 surge como o grupo de maior ticket médio, porém com a menor frequência (cerca de 1 vez ao mês). Este cluster poderia ser caracterizado como o grupo de clientes de uma grande família ou mesmo uma empresa informal (loja de sucos, etc).

Os Clusters 0 e 3 apresentam frequência e ticket semelhantes, contudo o cluster 3 se destaca pela maior recência entre todos os clusters, ou seja o grupo de clientes que não voltaram a fazer compra por muito tempo. O Cluster 2 por exemplo pode ser um cluster de interesee para uma campanha de marketing digital, para tentar fazer esses clientes retornarem as compras.

Para o propósito do estudo a análise de cestas foi focada no Cluster de maior frequência (Cluster 2), e esta análise revelou algumas associações de compra que fizeram sentido, como a compra de alho e batata e algumas frutas que são compradas em conjunto como banana e laranja. Contudo a relevância de campanhas de promoção orientadas a esse oe outros clientes só realmente poderia ser de fato comprovada com a realização de Testes A/B, o que não pôde ser feito.

### 4. Conclusões

Foi possível através de uma abordagem de aprendizado de máquina não supervisionada, usando as dimensões construidas de RFM e o métrodo de clusterização k-means construindo, identificar perfis distintos de compra para os clientes e classifica-los quanto a esse perfil. Esse é um método poderoso para ajudar um negócio como o varejo a melhor qualificar seus clientes e melhorar direcionar os esforços de marketing, não só com possível resultados positivos na geração de receita como na melhor eficiência do gasto de marketing, promoções, etc.

Com a classificação dos clientes, foi possível então entender através de regras de associação e aplicação do algoritmo Apriori, quais seriam os produtos mais relevantes para o cluster mais frequente de clientes. Com essa informação seria possível ao departamento de marketing determinar uma campanha de promoção customizada para esses clientes, orientando o desconto para um conjunto de produtos que poderiam alavancar outros produtos.

Esse estudo prova que essas técnicas são poderosas para trazer um melhor entendimento sobre os clientes e mais ainda, que podem ser implantadas com baixo custo de implementação para diversos tipo de varejo.

---

Matrícula: 191.671.035

Pontifícia Universidade Católica do Rio de Janeiro

Curso de Pós Graduação *Business Intelligence Master*
